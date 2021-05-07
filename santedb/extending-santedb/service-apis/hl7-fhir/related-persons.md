# Related Persons

This page discusses the manner in which FHIR RelatedPerson resources are handled and the various caveats of how those relate to the iCDR relationships.

## CDR Relationships

The CDR storage model support robust linkages between patients and persons. Some SanteDB services such as the Immunization Management Service \(IMS\) represent relationships between non-patient persons as a direct relationship between an instance of a Patient entity and a Person entity with a relationship type. 

![](../../../../.gitbook/assets/image%20%28202%29.png)

This example illustrates a simple non-patient entity \(Sarah Smith\) is the mother of a Patient \(Baby Joe Smith\).

Additionally, the CDR also supports the direct linking of patient entities to other patient entities in relationships. The illustration below illustrates a patient entity \(Sarah Smith\) is the mother of Patient \(Baby Joe Smith\).

![](../../../../.gitbook/assets/image%20%28207%29.png)

## FHIR Relationships

### Simple Relationships

The manner in which HL7 FHIR views patient relationships is reversed from the CDR's view of relationships. Primarily, HL7 FHIR would represent a non-patient person relationship to a patient as.

![](../../../../.gitbook/assets/image%20%28203%29.png)

In effect, the FHIR resource RelatedPerson is a mashup of a Person and an EntityRelationship, as the RelatedPerson contains elements of both objects.

![](../../../../.gitbook/assets/image%20%28205%29.png)

The CDR handles these relationship types automatically. When querying from FHIR with `_revInclude=RelatedPerson:patient` , the CDR will interpret either of these relationships and will construct the appropriate response messages for broadcasts and searches. 

The CDR will treat the target of the personal relationship as a Person. Since the CDR support hierarchy and Patient is a Patient, this translation is transparent to the FHIR interface. The CDR treats the instance of RelatedPerson as the EntityRelationship instance between the two entities. The CDR's FHIR plugin will reverse the relationship to ensure that the FHIR RelatedPerson references is correctly associated.

{% hint style="info" %}
The reason the RelatedPerson is linked to the EntityRelationship is a single Person may have multiple relationships \(for example, a mother of two children\). However, in FHIR a RelatedPerson may only have a single relationship between a Person and a Patient.
{% endhint %}

This behaviour matches the HL7 processor when an NK1 segment is present. For example, this HL7 message

```text
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

![](../../../../.gitbook/assets/image%20%28210%29.png)

### Complex Relationships

Relationships between Patients in FHIR are slightly more complex, take for example, a scenario where a Sarah Smith is a patient and is related to Baby Joe Smith. In FHIR the structure of this message would be as follows.

![](../../../../.gitbook/assets/image%20%28208%29.png)

The HL7 FHIR processor on a read will not reproduce this when a patient is read from the database and is directly related to another patient. Instead the simple case of representation is performed on a query.

When creating or updating a related person in this manner the following structure is created in the RIM structure.

![](../../../../.gitbook/assets/image%20%28201%29.png)

This structure is also created from the HL7v2 process when an NK1 segment points at a previously registered PID segment. For example, the following HL7v2 structure also creates a similar structure as the FHIR interface.

```text
MSH|^~\&|TEST|TEST|CR1|MOH_CAAT|20211104174451|DEVICESECRET|ADT^A01^ADT_A01||P|2.3.1
EVN||20211020
PID|||234^^^TEST||SMITH^SARAH|19840503|M

MSH|^~\&|TEST|TEST|CR1|MOH_CAAT|20211104174451|DEVICESECRET|ADT^A01^ADT_A01||P|2.3.1
EVN||20211020
PID|||HL7-3^^^TEST||SMITH^BABY JOE^^^^^L|SMITH^SARAH^^^^^|20210123|M|||||||||||
NK1||SMITH^SARAH|MTH||||E|||||||||19840503|||US|EN||||||||||||234^^^TEST
```

This structure will indicate that a patient is admitted to hospital \(Sarah Smith\) and then is linked to Baby Joe Smith as a next of kin. In FHIR this structure is represented as.

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

More complex relationships between patients and related persons are supported in the SanteDB CDR. For example, a single patient with two children in a FHIR bundle would be represented as:

![](../../../../.gitbook/assets/image%20%28204%29.png)

If both RelatedPerson/1 and RelatedPerson/2 carry the same logical identifier in the &lt;identifier&gt; element of the RelatedPerson the structure illustrated below is created in the CDR since the "Person" the related-person 

![](../../../../.gitbook/assets/image%20%28209%29.png)

However if it is not possible to identify RelatedPerson/1 and RelatedPerson/2 as the same person, the structure created in the CDR will be as illustrated.

![](../../../../.gitbook/assets/image%20%28211%29.png)

