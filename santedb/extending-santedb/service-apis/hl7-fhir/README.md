# HL7 FHIR

SanteDB's HL7 FHIR interfaces are handled through the `SanteDB.Messaging.FHIR.FhirMessageHandler` service and are configured via the `FhirConfigurationSection`.

## FHIR Implementation

Unlike CDRs which assume FHIR as the basis of their data storage throughout the stack, SanteDB treats FHIR as an edge messaging format. Therefore FHIR resource requests are considered **transient** and are never persisted into the database.

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
                "id" : 3
            }
        }
    ]
```

In SanteDB this fullUrl is replaced with the internal URL on the SanteDB server once submitted. The FHIR message processor only keeps track of `http://example.com/fhir/Patient/3` in order to resolve references within the same message transaction. 

Furthermore, the id element \(valued with 3 in the example\) is also not stored, and is only used to resolve entities within the transient submission.

{% hint style="info" %}
There is a discussion within the SanteDB development community on whether original URLs and identifiers should be stored in a non-unique identity domain on the SanteDB server or as a tag. 
{% endhint %}

### Offsite Resource Links

In FHIR, it is possible to link to clinical data hosted offsite, or on another server. There are several reasons why this is a bad practice \(including remote server outages, data integrity, etc.\). 

Consider the following request to create a patient

```text
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

When submitting this resource to the SanteDB FHIR interface, you will receive an error indicating that the managing organization is not known to SanteDB. You can resolve this by either including the organization information in the submission:

```javascript
{
    "resourceType" : "Bundle",
    "entry" : [
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
        },
        {
            "fullUrl" : "http://some-other-registry.org/fhir/Organization/123",
            "resource" : {
                // data fetched from Organization
            }
        }
    ]
}
```

Or you can manually register the Organization using the REST api and then including the logical identifier as the resource link:

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

However, the following, alternate form of reference link is also permitted:

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



