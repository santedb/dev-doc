# Related Persons

This page discusses the manner in which FHIR RelatedPerson resources are handled and the various caveats of how those relate to the iCDR relationships.

## CDR Relationships

The CDR storage model support robust linkages between patients and persons. Some SanteDB services such as the Immunization Management Service (IMS) represent relationships between non-patient persons as a direct relationship between an instance of a Patient entity and a Person entity with a relationship type. 

![Patient Baby Joe Smith has a mother (MTH) Person Sarah Smith](<../../../../../.gitbook/assets/image (393).png>)

This example illustrates a simple non-patient entity (Sarah Smith) is the mother of a Patient (Baby Joe Smith).

Additionally, the CDR also supports the direct linking of patient entities to other patient entities in relationships. The illustration below illustrates a patient entity (Sarah Smith) is the mother of Patient (Baby Joe Smith).

![Patient Baby Joe Smith has a mother (MTH) Patient Sarah Smith](<../../../../../.gitbook/assets/image (392).png>)

This relationship works because in SanteDB a Patient **is a** Person.

## FHIR Relationships

In FHIR, the `RelatedPerson` resource is used to represent a related person. Unlike SanteDB's RIM model, FHIR's `RelatedPerson` maps to one of the following internal concepts in SanteDB:

* A combination of `Person` and `EntityRelationship` where the `Person` may only contain one relationship to one `Patient`, or
* An `EntityRelationship` only, where only the relationship type is expressed.

A `RelatedPerson` represents a combination of `Person`and `EntityRelationship` when it is expressed as:

```javascript
{
  "resourceType": "RelatedPerson",
  "id": "123",
  "patient": {
    "reference": "Patient/321"
  },
  "relationship": [
    {
      "coding": [
        {
          "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
          "code": "MTH"
        }
      ]
    }
  ],
  "name": [
    {
      "use": "usual",
      "given": [
        "SU MYAT LWIN"
      ]
    }
  ],
  "gender": "female"
}
```

This condition is described in the section Simple Relationships on this page. However, a `RelatedPerson` is only an `EntityRelationship` when it is represented as:

```javascript
"entry": [
  ...
  {
    "fullUrl": "RelatedPerson/123",
    "resource": {
      "resourceType": "RelatedPerson",
      "id": "123",
      "patient": {
        "reference": "Patient/ohie-cr-05-20-fhir-baby"
      },
      "relationship": [
        {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
              "code": "MTH"
            }
          ]
        }
      ]
    }
  },
  {
    "fullUrl": "Patient/123",
    "resource": {
      "resourceType": "Patient",
      "id": "123",
      "name": [
        {
          "use": "maiden",
          "given": [
            "SU MYAT LWIN"
          ]
        }
      ],
      "gender": "female",
      "birthDate": "1984-05-25",
      "link": [
        {
          "other": {
            "reference":"RelatedPerson/123"
          },
          "type": "seealso"
        }
      ]
    }
  }
]
```

The behavior of the iCDR is described in Complex Relationships in this page.

### Simple Relationships

The manner in which HL7 FHIR views patient relationships is reversed from the CDR's view of relationships. Primarily, HL7 FHIR would represent a non-patient person relationship to a patient as.

![](<../../../../../.gitbook/assets/image (203).png>)

In effect, the FHIR resource `RelatedPerson` is a mashup of a `Person` and an `EntityRelationship`, as the `RelatedPerson` contains elements of both objects.

![Relationships are Reversed from FHIR to SanteDB RIM](<../../../../../.gitbook/assets/image (389).png>)

The CDR handles these relationship types automatically. When querying from FHIR with `_revInclude=RelatedPerson:patient` , the CDR will interpret either of these relationships and will construct the appropriate response messages for broadcasts and searches. 

The CDR will treat the target of the personal relationship as a Person. Since the CDR support hierarchy and Patient is a Patient, this translation is transparent to the FHIR interface. The CDR treats the instance of `RelatedPerson` as the `EntityRelationship` instance between the two entities. The CDR's FHIR plugin will reverse the relationship to ensure that the FHIR `RelatedPerson` references is correctly associated.

{% hint style="info" %}
The reason the RelatedPerson is linked to the EntityRelationship is a single Person may have multiple relationships (for example, a mother of two children). However, in FHIR a RelatedPerson may only have a single relationship between a Person and a Patient.
{% endhint %}

This behaviour matches the HL7 processor when an NK1 segment is present. For example, this HL7 message

```
MSH|^~\&|TEST|TEST|CR1|MOH_CAAT|20211104174451|DEVICESECRET|ADT^A01^ADT_A01||P|2.3.1
EVN||20211020
PID|||HL7-3^^^TEST||SMITH^BABY JOE^^^^^L|SMITH^SARAH^^^^^|20210123|M|||||||||||
NK1||SMITH^SARAH|MTH||||E|||||||||19840503|||US|EN||||||||||||234^^^TEST
```

And this FHIR message

```javascript
{
  "resourceType": "Bundle",
  "type": "transaction",
  "entry": [
    {
      "fullUrl": "Patient/1",
      "resource": {
        "resourceType": "Patient",
        "id": "1",
        "active": true,
        "identifier": [
          {
            "use": "official",
            "system": "http://santedb.org/fhir/test",
            "value": "HL7-3"
          }
        ],
        "name": [
          {
            "use": "usual",
            "family": "SMITH",
            "given": [
              "BABY", "JOE"
            ]
          }
        ],
        "gender": "male",
        "birthDate": "2021-01-23"
      },
      "request": {
        "method": "POST",
        "url": "Patient/1"
      }
    },
    {
      "fullUrl": "RelatedPerson/1",
      "resource": {
        "resourceType": "RelatedPerson",
        "id": "1",
        "patient": {
          "reference": "Patient/1"
        },
        "relationship": [
          {
            "coding": [
              {
                "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
                "code": "MTH"
              }
            ]
          }
        ],
        "name": [
          {
            "use": "usual",
            "family": "SMITH",
            "given": [
              "SARAH"
            ]
          }
        ],
        "gender": "female"
      },
      "request": {
        "method": "POST",
        "url": "RelatedPerson/1"
      }
    }
  ]
}
```

Will both result in this structure in the database.

![FHIR structure mapped to the RIM](<../../../../../.gitbook/assets/image (390).png>)

### Complex Relationships

Relationships between Patients in FHIR are slightly more complex, take for example, a scenario where a Sarah Smith is a patient and is related to Baby Joe Smith. In FHIR the structure of this message would be as follows.

![](<../../../../../.gitbook/assets/image (208).png>)

The HL7 FHIR processor on a read will not reproduce this when a patient is read from the database and is directly related to another patient. Instead the simple case of representation is performed on a query.

When creating or updating a related person in this manner the following structure is created in the RIM structure.

![](<../../../../../.gitbook/assets/image (391).png>)

This structure is also created from the HL7v2 process when an NK1 segment points at a previously registered PID segment. For example, the following HL7v2 structure also creates a similar structure as the FHIR interface.

```
MSH|^~\&|TEST|TEST|CR1|MOH_CAAT|20211104174451|DEVICESECRET|ADT^A01^ADT_A01||P|2.3.1
EVN||20211020
PID|||234^^^TEST||SMITH^SARAH|19840503|M

MSH|^~\&|TEST|TEST|CR1|MOH_CAAT|20211104174451|DEVICESECRET|ADT^A01^ADT_A01||P|2.3.1
EVN||20211020
PID|||HL7-3^^^TEST||SMITH^BABY JOE^^^^^L|SMITH^SARAH^^^^^|20210123|M|||||||||||
NK1||SMITH^SARAH|MTH||||E|||||||||19840503|||US|EN||||||||||||234^^^TEST
```

This structure will indicate that a patient is admitted to hospital (Sarah Smith) and then is linked to Baby Joe Smith as a next of kin. In FHIR this structure is represented as.

```javascript
{
  "resourceType": "Bundle",
  "type": "transaction",
  "entry": [
    {
      "fullUrl": "Patient/1",
      "resource": {
        "resourceType": "Patient",
        "id": "1",
        "active": true,
        "identifier": [
          {
            "use": "official",
            "system": "http://santedb.org/fhir/test",
            "value": "HL7-3"
          }
        ],
        "name": [
          {
            "use": "usual",
            "family": "SMITH",
            "given": [
              "BABY", "JOE"
            ]
          }
        ],
        "gender": "male",
        "birthDate": "2021-01-23"
      },
      "request": {
        "method": "POST",
        "url": "Patient/1"
      }
    },
    {
      "fullUrl": "RelatedPerson/1",
      "resource": {
        "resourceType": "RelatedPerson",
        "id": "1",
        "patient": {
          "reference": "Patient/1"
        },
        "relationship": [
          {
            "coding": [
              {
                "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
                "code": "MTH"
              }
            ]
          }
        ]
      },
      "request": {
        "method": "POST",
        "url": "RelatedPerson/1"
      }
    },
    {
      "fullUrl": "Patient/2",
      "resource": {
        "resourceType": "Patient",
        "id": "2",
        "active": true,
        "identifier": [
          {
            "use": "official",
            "system": "http://santedb.org/fhir/test",
            "value": "0234"
          }
        ],
        "name": [
          {
            "use": "usual",
            "family": "SMITH",
            "given": [
              "SARAH"
            ]
          }
        ],
        "gender": "male",
        "birthDate": "1984-05-03",
        "link": {
          "type" : "seealso",
          "other" : {
            "reference": "RelatedPerson/1"
          }
      },
      "request": {
        "method": "POST",
        "url": "Patient/1"
      }
    }
  ]
}
```

## Special Implementation Notes for Related Person

* When querying a patient which has a relationship with another patient (for example, querying for `?identifier=HL7-3` ) you can use `_revInclude=RelatedPerson:patient` to join a RelatedPerson instance, however the included `RelatedPerson` instance will be represented as a simple relationship rather than a complex relationship.
* It is not possible to perform a `_revInclude=Patient:link` on order to retrieve patient information about the `RelatedPerson` , this is because there is no relationship or link per-se between the `Person` and `Patient`, in SanteDB **they are the same resource**
* The `id` and `fullUrl` of the `RelatedPerson` is the `id` property of the `EntityRelationship` rather than the `Person`. This is because in FHIR a `RelatedPerson` can have **exactly one** relationship to **exactly one** `Patient`, however in SanteDB RIM a `Person` can have **infinite** relationships to **infinite **`Patient` resources.
* When querying directly for a `Patient ` instance on the FHIR interface, you may see one or more `link` properties such as listed below, this link information is provided to indicate there exists a relationship where the patient is a target of a relationship.

```markup
<link>
      <other>
         <reference value="RelatedPerson/26d3c0e4-730e-41eb-98a2-52b5ac97cd2c"/>
         <display value="26d3c0e4-730e-41eb-98a2-52b5ac97cd2c"/>
      </other>
      <type value="seealso"/>
   </link>
```

{% hint style="info" %}
When MDM is enabled, the **Master/Golden** record is returned on queries, since no relationships can exists between a local to a master the master results will not return seealso links to RelatedPerson instances (since they are not pointed at data).
{% endhint %}
