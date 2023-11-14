---
description: Patient Merge Governance / Security Enforcement
---

# TEST: OHIE-CR-09-FHIR

This test ensures that the Client Registry is capable of protecting identities from being merged/manipulated by sources which do not have authority over the records. For example, if `HOSPITAL_GREEN` instructs the Client Registry to merge records from `HOSPITAL_RED` , the Client Registry should block/prevent the merge from occurring, or should take on appropriate alternate actions.

{% hint style="info" %}
This test is based on governance rules rather than syntactic or semantic interpretation of a message. Therefore, some Client Registries or deployments may permit the actions and cross-domain merges of patient identity.
{% endhint %}

## Discussion

It is generally bad practice to allow clients full control over merging/de-activating records on the server since this requires each client communicating with the PMIR service to properly implement and govern merges. SanteDB has three different types of merge:

* LOCAL>MASTER: In which a flagged candidate `LOCAL` record is reconciled and linked/merged with an appropriate `MASTER` record. Clients which make these calls are required to have the `Write MDM Master` permission.&#x20;
* LOCAL>LOCAL: In which a client indicates that a registration they have previously sent is a duplicate of another record they had previously sent. This action requires no special permissions and is the default method of using a `replaces` link.
* MASTER>MASTER: In which two golden or `MASTER` records are merged. This process includes the migration of all local references, and the record from truth from one master (the victim) to another (the survivor). Generally this merge is not permitted by clients unless the `Merge MDM Master` permissions is granted (which is bad practice as it bypasses all governance controls on the server).

These merge strategies and the conditions under which they are permitted are described in the [Master Data Management](../../../../../../../../santedb/data-and-information-architecture/data-storage-patterns/master-data-storage.md#merging-linking) architecture article.

Furthermore SanteDB requires establishing ownership over a particular `LOCAL` record in order to determine if a source is permitted to merge two records. Generally, source `HOSPITAL_A` is only permitted to indicate merges of data only submitted from `HOSPITAL_A` and should not allow `HOSPITAL_B` records to be merged into `HOSPITAL_A`.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-04](test-ohie-cr-04-fhir.md) and [TEST: OHIE-CR-06](test-ohie-cr-06-fhir.md) have been run.

## Authenticate as TEST\_HARNESS\_FHIR\_A

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness-a account.

```http
POST http://localhost:8080/auth/oauth2_token HTTP/1.1
Accept-Encoding: gzip,deflate
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 94
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

grant_type=client_credentials&scope=*&client_secret=TEST_HARNESS&client_id=TEST_HARNESS_FHIR_A
```

## Register New Patient Identity in TEST\_A

The test harness sends an authenticated request to create a new patient with a new identifier in TEST\_A domain. Patient details:

* Identifier `FHRA-090` in `http://ohie.org/test/test_a`&#x20;
* Identifier `NID090` in `http://ohie.org/test/nid`&#x20;
* Name: BLOCKED MERGE JONES
* Gender: Female
* DOB: 1989-02-12

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-09-10-fhir",
    "active": true,
    "identifier": [
      {
        "use": "official",
        "type": {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
              "code": "PI"
            }
          ]
        },
        "system": "http://ohie.org/test/test_a",
        "value": "FHRA-090",
        "assigner": {
          "display": "Test Harness A Patient Identity"
        }
      },
      {
        "use":"usual",
        "system": "http://ohie.org/test/nhid",
        "value":"NID090"
      }
    ],
    "name": [
      {
        "use": "official",
        "family": "JONES",
        "given": [
          "BLOCKED","MERGE"
        ]
      }
    ],
    "gender": "female",
    "birthDate": "1989-02-12",
  }
```

### Expected Behaviour

| Requirement | Option    | Description                                                    |
| ----------- | --------- | -------------------------------------------------------------- |
| MUST        | PMIR Only | Return MessageHeader with response.code = ok                   |
| MUST        |           | Return HTTP code of 201 Created                                |
| SHOULD      | PMIR Only | Include an OperationOutcome entry in the response              |
| SHOULD      |           | Include a Patient entry in response containing created patient |
| SHOULD      |           | Include a link to the master identity with code refer          |

## Authenticate as TEST\_HARNESS\_FHIR\_B

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness-a account.

```http
POST http://localhost:8080/auth/oauth2_token HTTP/1.1
Accept-Encoding: gzip,deflate
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 94
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)



grant_type=client_credentials&scope=*&client_secret=TEST_HARNESS&client_id=TEST_HARNESS_FHIR_B
```

## Register New Patient Identity in TEST\_B

The test harness sends an authenticated request to create a new patient with a new identifier in TEST\_B domain. Patient details:

* Identifier `FHRB-090` in `http://ohie.org/test/test_b` with use `official`
* Identifier `NID091` in `http://ohie.org/test/nid`&#x20;
* Name: BLOCK MERGE JONES
* Gender: female

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-09-20-fhir",
    "active": true,
    "identifier": [
      {
        "use": "official",
        "type": {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
              "code": "PI"
            }
          ]
        },
        "system": "http://ohie.org/test/test_b",
        "value": "FHRB-090",
        "assigner": {
          "display": "Test Harness B Patient Identity"
        }
      },
      {
        "use":"usual",
        "system": "http://ohie.org/test/nid",
        "value":"NID091"
      }
    ],
    "name": [
      {
        "use": "official",
        "family": "JONES",
        "given": [
          "BLOCK","MERGE"
        ]
      }
    ],
    "gender": "female"
  }
```

### Expected Behaviour

| Requirement | Option    | Description                                                    |
| ----------- | --------- | -------------------------------------------------------------- |
| MUST        | PMIR Only | Return MessageHeader with response.code = ok                   |
| MUST        |           | Return HTTP code of 201 Created                                |
| SHOULD      | PMIR Only | Include an OperationOutcome entry in the response              |
| SHOULD      |           | Include a Patient entry in response containing created patient |
| SHOULD      |           | Include a link to the master identity with code refer          |

## Attempt Cross-Domain Merge

In this test step, the test harness will attempt (while authenticated as `TEST_HARNESS_FHIR_B`) to merge the record created by another sender. This type of merge is generally not permitted from a data governance perspective (as harness B would have no authoritative control over data from harness A).

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-09-30-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/harness"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-09-30-fhir"
          }
        ],
        "destination": [
          {
            "endpoint": "http://ohie.org/test/endpoint/Bundle"
          }
        ]
      }
    },
    {
      "fullUrl": "http://ohie.org/test/Bundle/ohie-cr-09-30-fhir",
      "resource": {
        "resourceType": "Bundle",
        "id":"ohie-cr-09-30-fhir",
        "type": "history",
        "entry": [
          {
            "fullUrl": "http://ohie.org/test/Patient/ohie-cr-09-30-fhir",
            "resource": {
              "resourceType": "Patient",
              "id": "ohie-cr-09-20-fhir",
              "active": false,
              "identifier": [
                {
                  "use": "official",
                  "type": {
                    "coding": [
                      {
                        "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
                        "code": "PI"
                      }
                    ]
                  },
                  "system": "http://ohie.org/test/test_b",
                  "value": "FHRB-090",
                  "assigner": {
                    "display": "Test Harness B Patient Identity"
                  }
                }
              ],
              "link": [
                {
                  "other": {
                    "type": "Patient",
                    "identifier": {
                      "value": "FHRA-090",
                      "system": "http://ohie.org/test/test_a"
                    }
                  },
                  "type": "replaced-by"
                }
              ]
            },
            "request": {
              "method": "PUT",
              "url": "Patient/ohie-cr-09-30-fhir"
            },
            "response": {
              "status":"200"
            }
          }
        ]
      }
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option | Description                                                                                                                   |
| ----------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| MUST        |        | Return HTTP code of 422 UNPROCESSABLE ENTITY or 400 BAD REQUEST or 403 FORBIDDEN                                              |
| MUST        |        | Return a `Bundle` with a `MessageHeader` carrying a `response` code of `fatal-error`                                          |
| MUST        |        | Carry an `OperationOutcome` resource which indicates that the merge could not be completed due to invalid authority to merge. |

