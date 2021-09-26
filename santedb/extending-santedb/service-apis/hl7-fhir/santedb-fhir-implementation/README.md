# Implementation Details

Unlike CDRs which use FHIR as the basis of their data storage throughout the stack, SanteDB treats FHIR as an edge messaging format. Therefore FHIR resource requests are considered **transient** and are never persisted into the database.

Because of this, there are several implementation notes which are important to remember when interacting with the SanteDB FHIR service handlers.

### Resource URLS and ID

When submitting a FHIR bundle, each entry in the bundle may contain a `fullUrl` property which point to an absolute URL where the resource originated and/or was referenced. For example:

```javascript
{
    "resourceType" : "Bundle",
    "entry" : [
        {
            "fullUrl" : "http://example.com/fhir/Patient/3",
            "resource": {
                "resourceType" : "Patient",
                "id" : "3"
            }
        }
    ]
```

In SanteDB this fullUrl is replaced with the internal URL on the SanteDB server once submitted. For example, after submission `Patient/3` would carry a `fullUrl` of `http://santedb_server/fhir/Patient/95569551-5abd-4484-be52-4c6986c4beb7` and an `id` of `95569551-5abd-4484-be52-4c6986c4beb7` . 

The FHIR message processor only tracks `http://example.com/fhir/Patient/3` in order to resolve references within the same message transaction, this is not stored in the database unless the identifier is a UUID in which case the `id` element will be used as the suggested UUID for inserting the patient \(i.e. update if the UUID exists, or use the UUID if it doesn't\). 

There are several reasons that SanteDB doesn't store this information:

1. The `fullUrl` may be a fully qualified URL, may be an OID, a UUID, or a relative URL which have different semantic meanings in the iCDR instance.
2. It is nearly impossible to determine if any random client is sending`id` from the perspective of itself \(i.e. my internal reference for this record is X and I am sharing it with the server\), or if it is from the perspective of the iCDR \(i.e. I have fetched this resource from you and am using your identifier\). 
3. Simple structured identifiers and fullUrls have no concrete meaning , for example `SYSTEM_A` sending a `Patient` with a relative URL of`Patient/1` and `SYSTEM_B` sending `Patient/1`. The actual record being updated cannot be reliably resolved with ID `1` or even `Patient/1` so mis-identification is a serious risk.
4. While it would be possible to store the `fullUrl` for an object stored as a bundle, objects submitted via simple `POST` operations via REST to the SanteDB iCDR instance would not have this contextual identifier, and would merely carry an `id` element, making referencing the object impossible.

{% hint style="info" %}
The behavior of the logical id and full URL are aligned with the [FHIR behaviors specified on Logical ID](https://www.hl7.org/fhir/R4/resource.html#id) , it is recommended that production deployments use [business identifiers ](https://www.hl7.org/fhir/R4/resource.html#identifiers)when referencing objects in FHIR.
{% endhint %}

### Offsite Resource Links

In FHIR, it is possible to link to clinical data hosted offsite, or on another server. There are several reasons why this is a bad practice:

* Internal processes within SanteDB wouldn't have information necessary to action the object \(such as matching, de-duplication, etc.\)
* There would be no way for the dCDR instances to actually acquire the information to populate the user interface since offsite references **assume** that an internet connection is available to fetch the resource
* There is an assumption made that the offsite server will be accessible at all times from all clients which may consume the information, this is often not the case.
* There is a dependency on another system to be present, the identifier / resource to be valid \(not removed as part of a merge/move operation, etc.\)

Consider the following request to create a patient

```javascript
{
    "resourceType":"Patient",
    "name": [
        "use":"official",
        "given": [ "JOHN" ],
        "family": "SMITH"
    ],
    "managingOrganization" : {
        "reference" : "http://some-other-registry.org/fhir/Organization/123"
    }
}
```

When submitting this resource to the SanteDB FHIR interface, you will receive an error indicating that the managing organization is not known to SanteDB. 

```javascript
{
   "resourceType": "OperationOutcome",
   "id": "8441e711-6d63-426c-95b6-c3289f9866a7",
   "issue": [            {
      "severity": "error",
      "code": "exception",
      "diagnostics": "Could not find http://some-other-registry.org/fhir/Organization/123 as a previous entry in this submission. Cannot resolve from database unless reference is either urn:uuid:UUID or Type/UUID"
   }]
}
```

You can resolve this by either including the organization information in the submission:

```javascript
{
    "resourceType" : "Bundle",
    "entry" : [
        {
            "fullUrl" : "http://some-other-registry.org/fhir/Organization/123",
            "resource" : {
                // data fetched from Organization
            }
        },
        {
            "fullUrl" : "http://example.com/fhir/Patient/3",
            "resource": {
                "resourceType":"Patient",
                "name": [
                    "use":"official",
                    "given": [ "JOHN" ],
                    "family": "SMITH"
                ],
                "managingOrganization" : {
                    "reference" : "http://some-other-registry.org/fhir/Organization/123"
                }
            }
        }
    ]
}
```

Or you can manually register the Organization using the REST api and then including the logical identifier as the resource link or UUID within SanteDB's database:

```javascript
{
    "resourceType":"Patient",
    "name": [
        "use":"official",
        "given": [ "JOHN" ],
        "family": "SMITH"
    ],
    "managingOrganization" : {
        "identifier" : {
            "system" : "some-known-identity-domain",
            "value" : "some-known-identifier"
        }
    }
}
```

### FHIR References

In FHIR a `Reference` object is used to link two resources together in a role. This is similar to SanteDB's `EntityRelationship` class, with the limitation that `EntityRelationship` does not permit the linking of objects which are not stored within the SanteDB instance. 

#### Reference By UUID

Referencing an object by UUID is the most preferred mechanism of resource referencing. Resources which are linked by UUID are first cross referenced in the current processing scope \(the bundle\), followed by database linkage. Reference by UUID is commonly represented as:

```javascript
"someReference" : {
     "reference" : "Patient/bcddb6c7-2892-4b61-aec6-0dbdd718b792"
}
```

Alternately, if you're not picky about what the reference type is \(i.e. it could be any entity, but it is a known entity to SanteDB\) you can use a plain UUID reference:

```javascript
"someReference" : {
     "reference" : "urn:uuid:bcddb6c7-2892-4b61-aec6-0dbdd718b792"
}
```

You can also reference contained resources using a local reference:

```javascript
"contained": [
    {
        "resourceType":"RelatedPerson",
        "id":"123"
    }
], 
...
"someReference": {
    "reference":"#123"
}
```

Business identifier references are also supported by the reference resolver:

```javascript
"someReference" : {
     "type" : "Patient",
     "identifier": {
          "value": "bcddb6c7-2892-4b61-aec6-0dbdd718b792"
     }
}
```

#### Reference Bundle Object

Referencing an object which is being processed within the same scope is also permitted. The reference is subject to the following limitations:

1. The `reference` property must exactly match the `fullUrl` property in the bundle
2. The `reference` objects must exist **in order** , i.e. a `RelatedPerson` which has a reference of `Patient/1` must exist **after** the `Patient` ****with `fullUrl` of `Patient/1` in the bundle
3. No circular references are permitted \(i.e. `Patient/2` with `link` to `RelatedPerson/1` with a link to `Patient/1` which in-turn links to `Patient/2` \)

```javascript
"entry": [
  {
    "fullUrl": "Patient/1",
    "resource": {
      "resourceType": "Patient",
      "id": "1",
      ...
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
      ...
    }
  }
```

### Re-Submission of Unidentified Resources

Whenever a client system submits an unidentified resource to the SanteDB iCDR FHIR interface, SanteDB will create a new copy of that resource and generate a unique UUID for it. An unidentified resource is a resource which lacks any of:

* A full UUID as the `id` element of the resource
* A business identifier in the `identifier` element of the resource within a uniquely generated identity domain

For example, consider the registration of a patient and a related person:

```javascript
"entry": [
    {
      "fullUrl": "Patient/1",
      "resource": {
        "resourceType": "Patient",
        "id": "1",
        "name": [
          {
            "use": "usual",
            "given": [
              "JOHN"
            ]
          }
        ],
        "gender": "male",
        "birthDate": "2017-04-03"
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
            "given": [
              "MARY"
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
```

Upon sending this bundle to the server, the iCDR will create a new `Patient` \(example: `Patient/UUIDA`\) and a new `Person` \(example: `Person/UUIDB`\) which is related via an `EntityRelationship`. If a client re-submits this exact bundle, the iCDR will \(once again\) register a new `Patient` \(example: `Patient/UUIDC` \) and a new `Person` \(example: `Person/UUIDD`\).

If, however only one of the resources contained a reliable identifier, such as the patient in this example:

```javascript
"entry": [
    {
      "fullUrl": "Patient/1",
      "resource": {
        "resourceType": "Patient",
        "id": "1",
        "identifier": [
          {
            "system":"http://santedb.org/unique_domain",
            "value":"FHR-4040"
          }
        ],
        "name": [
          {
            "use": "usual",
            "given": [
              "JOHN"
            ]
          }
        ],
        "gender": "male",
        "birthDate": "2017-04-03"
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
            "given": [
              "MARY"
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
```

Then the behavior is modified such that an initial submission results in a `Patient` with business identifier `FHR-4040` \(example: `Patient/UUIDA`\) and a `Person` \(example: `Person/UUIDB`\) related to one another via an `EntityRelationship`.

If the client resubmits this bundle, the CDR is able to cross-reference the `Patient` \(as it has a business identifier of `FHR-4040`\) and would perform an update \(on `Patient/UUIDA`\) however since the `RelatedPerson` cannot be reliably referenced to a known object, a new `Person` would be created \(example: `Person/UUIDC`\) related to the `Patient` via an `EntityRelationship`.

The end state of this message would be:

* `Patient/UUIDA` exists with business identifier `FHR-4040`
* `Person/UUIDB` exists and is related via `EntityRelationship` as the `MOTHER` of `Patient/UUIDA`
* `Person/UUIDC` exists and is related via `EntityRelationship` as the `MOTHER` of `Patient/UUIDA`

The recommended manner to submit this bundle would be to either give both `Patient` and `RelatedPerson` a reliable business identifier:

```javascript
"entry": [
    {
      "fullUrl": "Patient/1",
      "resource": {
        "resourceType": "Patient",
        "id": "1",
        "identifier": [
          {
            "system":"http://santedb.org/unique_domain",
            "value":"FHR-4040"
          }
        ],
        ...
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
        "identifier": [
          {
            "system":"http://santedb.org/unique_domain",
            "value":"FHR-4041"
          }
        ]
        ...
      },
      "request": {
        "method": "POST",
        "url": "RelatedPerson/1"
      }
    }
```

Or to give each a UUID as their identifier:

```javascript
"entry": [
    {
      "fullUrl": "Patient/32bdc53f-0908-4e47-990b-43484ffc78bc",
      "resource": {
        "resourceType": "Patient",
        "id": "32bdc53f-0908-4e47-990b-43484ffc78bc",
        ...
      },
      "request": {
        "method": "POST",
        "url": "Patient/32bdc53f-0908-4e47-990b-43484ffc78bc"
      }
    },
    {
      "fullUrl": "RelatedPerson/95569551-5abd-4484-be52-4c6986c4beb7",
      "resource": {
        "resourceType": "RelatedPerson",
        "id": "95569551-5abd-4484-be52-4c6986c4beb7",
        "patient": {
          "reference": "Patient/32bdc53f-0908-4e47-990b-43484ffc78bc"
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
        ...
      },
      "request": {
        "method": "POST",
        "url": "RelatedPerson/95569551-5abd-4484-be52-4c6986c4beb7"
      }
    }
```

