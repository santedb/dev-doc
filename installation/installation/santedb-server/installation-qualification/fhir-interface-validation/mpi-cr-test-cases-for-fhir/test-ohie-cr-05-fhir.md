# TEST: OHIE-CR-05-FHIR

This test ensures that the receiver can create a record with minimally useful information linked to another person/patient. This is often useful when registering an infant demographic record where only date of birth, gender and mother's information is known.

{% hint style="info" %}
This test is a combination of TEST-OHIE-CR05 and TEST-OHIE-CR07 from the HL7v2 test suite.
{% endhint %}

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)
* [Integrating The Health Enterprise Patient Demographics Query for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PDQm.pdf)

## Discussion

A master patient index/client registry is often tasked with the storage of partial registration records and/or records which are only identifiable by their mother's information.&#x20;

Whereas this information can be registered in one message in HL7v2 (using mother's name and mother's identifier), this test requires the use of either:

* A FHIR transaction bundle to register a related person (the mother) and patient
* Two FHIR operations to register the patient and the related person (the mother)
* A PMIR message with the related person (the mother) and patient.

### FHIR Representation of Mother/Child Relationship

SanteMPI supports robust relationships between entities which cannot be easily expressed in FHIR. For example, there may be use cases where the mother is a patient (via delivery) at a hospital and the child is also a patient (receiving care at a NICU). Unfortunately, this type of relationship in FHIR is represented as the following structure:

```http
<Patient>
     <id>child</id>
</Patient>
<RelatedPerson>
     <id>rp-mother</id>
     <patient>
          <reference value="Patient/child"/>
     </patient>
</RelatedPerson>
<Patient>
     <id>pat-mother</id>
     <link>
          <other value="RelatedPerson/rp-mother"/>
          <type value="see-also"/>
     </link>
</Patient>
```

Unfortunately in SanteMPI this type of relationship can only be established when:

* The three resources are submitted as part of an entire bundle (such as a transaction bundle or PMIR operation)
* The Registration occurs on the REST interface such that:
  * Mother Patient is registered first with a concrete identifier in the `identifier` property
  * Baby Patient is registered next with a concrete identifier in the `identifier` property
  * Mother RelatedPerson is registered using the same concrete `identifier` as that used in step .

This test suite tests both methods of creating a mother/child relationship

## Pre-Conditions / Setup

Ensure that all pre-conditions for [OHIE-CR-02-FHIR](test-ohie-cr-02-fhir.md#pre-conditions-setup) have been completed.

## Authenticate as TEST\_HARNESS\_FHIR

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness-a account.

```http
POST http://localhost:8080/auth/oauth2_token HTTP/1.1
Accept-Encoding: gzip,deflate
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 87
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)


grant_type=client_credentials&scope=*&client_secret=TEST_HARNESS&client_id=TEST_HARNESS
```

## Register Mother / Child Demographics in Transaction Bundle

The test harness sends an authenticated request to create a child record with a mother's demographics as a simple related person.

* Identifier FHR-050 in http://ohie.org/test/test with use official
* Name: WIN MINH
* Gender: Male
* DOB: 2017-04-03

The mother is a simple Related Person with name SU MYAT LWIN.

{% hint style="info" %}
This test case does not use familial names to mimic contexts where only given names (no surnames) are present.
{% endhint %}

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-05-10-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness_b"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-05-10-fhir"
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
      "fullUrl": "Bundle/ohie-cr-05-10-fhir",
      "resource": {
        "resourceType": "Bundle",
        "type": "history",
        "entry": [
          {
            "fullUrl": "Patient/ohie-cr-05-10-fhir",
            "resource": {
              "resourceType": "Patient",
              "id": "ohie-cr-05-10-fhir",
              "active": true,
              "identifier": [
                {
                  "use": "official",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-050"
                }
              ],
              "name": [
                {
                  "use": "usual",
                  "given": [
                    "WIN MINH"
                  ]
                }
              ],
              "gender": "male",
              "birthDate": "2017-04-03"
              
            },
            "request": {
              "method": "POST",
              "url": "Patient/ohie-cr-05-10-fhir"
            }
          },
          {
            "fullUrl": "RelatedPerson/ohie-cr-05-10-fhir-mother",
            "resource": {
              "resourceType": "RelatedPerson",
              "id": "ohie-cr-05-10-fhir-mother",
              "patient": {
                "reference": "Patient/ohie-cr-05-10-fhir"
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
            },
            "request": {
              "method": "POST",
              "url": "RelatedPerson/ohie-cr-05-10-fhir-mother"
            }
          }
        ]
      }
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option    | Description                                                    |
| ----------- | --------- | -------------------------------------------------------------- |
| MUST        | PMIR Only | Return MessageHeader with response.code = ok                   |
| MUST        |           | Return HTTP code of 201 Created                                |
| SHOULD      | PMIR Only | Include an OperationOutcome entry in the response              |
| SHOULD      |           | Include a Patient entry in response containing created patient |
| SHOULD      |           | Include the RelatedPerson entry which was created              |
| SHOULD      |           | Include a link to the master identity with code refer          |

## Validate Child Patient Created

The test harness executes a query against the receiver to ensure the record was created domain

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-050&_revinclude=RelatedPerson%3Apatient HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                                                                  |
| ----------- | ------ | ---------------------------------------------------------------------------- |
| MUST        |        | Accept the message with HTTP 200 OK                                          |
| MUST        |        | Include a bundle with exactly 1 patient result                               |
| MUST        |        | Include a bundle with exactly 1 RelatedPerson result                         |
| MUST        |        | Contain a patient for WIN MINH                                               |
| MUST        |        | Have an identifier for FHR-050 in system http://ohie.org/test/test           |
| MUST        |        | Contain a RelatedPerson with name SU MYAT LWIN                               |
| SHOULD      |        | Contain one or more link entries with type seealso pointing to local records |

## Register Mother Patient and Newborn Demographics in Transaction Bundle

The test harness sends an authenticated request to create a newborn record with the mother's demographics. This test mimics registering a patient (the Mother) and a nameless newborn (the Baby) in one transaction.&#x20;

Patient (Mother) details:

* Identifier `FHR-052` in `http://ohie.org/test/test` with use `official`
* Name: SARAH ABELS
* Gender: Female
* DOB: 1984-05-25

Newborn information:

* Identifier `FHR-051` in `http://ohie.org/test/test`
* Gender: Female
* DOB: 2021-04-25

{% hint style="info" %}
The bundle portrayed is using type `history` and is intended to be tested as part of a PMIR payload. You can also use the bundle as a simple POST of a transaction.&#x20;
{% endhint %}

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-05-20-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-05-20-fhir"
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
      "fullUrl": "Bundle/ohie-cr-05-20-fhir",
      "resource": {
        "resourceType": "Bundle",
        "type": "history",
        "entry": [
          {
            "fullUrl": "Patient/ohie-cr-05-20-fhir-baby",
            "resource": {
              "resourceType": "Patient",
              "id": "ohie-cr-05-20-fhir-baby",
              "active": true,
              "identifier": [
                {
                  "use": "official",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-051"
                }
              ],
              "gender": "female",
              "birthDate": "2021-04-25"
            },
            "request": {
              "method": "POST",
              "url": "Patient/ohie-cr-05-20-fhir-baby"
            }
          },
          {
            "fullUrl": "RelatedPerson/ohie-cr-05-20-fhir-mother-rp",
            "resource": {
              "resourceType": "RelatedPerson",
              "id": "ohie-cr-05-10-fhir-mother-rp",
              "identifier": [
                {
                  "use": "official",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-052"
                }
              ],
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
            },
            "request": {
              "method": "POST",
              "url": "RelatedPerson/ohie-cr-05-20-fhir-mother-rp"
            }
          },
          {
            "fullUrl": "Patient/ohie-cr-05-20-fhir-mother",
            "resource": {
              "resourceType": "Patient",
              "id": "ohie-cr-05-10-fhir-mother",
              "identifier": [
                {
                  "use": "official",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-052"
                }
              ],
              "name": [
                {
                  "use": "maiden",
                  "family": "Abels",
                  "given": [
                    "Sarah"
                  ]
                }
              ],
              "gender": "female",
              "birthDate": "1984-05-25",
              "link": [
                {
                  "other": {
                    "reference":"RelatedPerson/ohie-cr-05-20-fhir-mother-rp"
                  },
                  "type": "seealso"
                }
              ]
            },
            "request": {
              "method": "POST",
              "url": "Patient/ohie-cr-05-20-fhir-mother"
            }
          }
        ]
      }
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option    | Description                                                                                               |
| ----------- | --------- | --------------------------------------------------------------------------------------------------------- |
| MUST        | PMIR Only | Return MessageHeader with response.code = ok                                                              |
| MUST        |           | Return HTTP code of 201 Created                                                                           |
| SHOULD      | PMIR Only | Include an OperationOutcome entry in the response                                                         |
| SHOULD      |           | <p>Include a Patient entry in response containing created patients for </p><p>the newborn and mother.</p> |
| SHOULD      |           | Include a link to the master identity with code refer                                                     |

## Validate Newborn Patient Created with Mother Related Person

The test harness executes a query against the receiver to ensure the record was created domain

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-051&_revinclude=RelatedPerson%3Apatient HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                  |
| ----------- | ------ | ---------------------------------------------------------------------------- |
| MUST        |        | Accept the message with HTTP 200 OK                                          |
| MUST        |        | Include a bundle with exactly 1 patient result.                              |
| MUST        |        | Contain the nameless newborn patient details (validated by Gender and DOB)   |
| MUST        |        | Have an identifier for FHR-051 in system http://ohie.org/test/test           |
| MUST        |        | Have a RelatedPerson with identifier FHR-052 for SARAH ABELS                 |
| SHOULD      |        | Contain one or more link entries with type seealso pointing to local records |

## Validate Mother Patient Created&#x20;

The test harness will query by the identifier of the mother to validate that the receiver created the mother record for a patient.

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-051&_revinclude=RelatedPerson%3Apatient HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                  |
| ----------- | ------ | ---------------------------------------------------------------------------- |
| MUST        |        | Accept the message with HTTP 200 OK                                          |
| MUST        |        | Include a bundle with exactly 1 patient result.                              |
| MUST        |        | Contain the mother  patient details  (name of SARAH ABELS)                   |
| MUST        |        | Have an identifier for FHR-052 in system http://ohie.org/test/test           |
| SHOULD      |        | Contain one or more link entries with type seealso pointing to local records |

## Patient Demographics Query for Mobile Paediatric Query

The test harness will execute a query on the patient resource and will validate that the client registry understands the extended `mothersMaidenName` parameter supplied.

```http
GET http://localhost:8080/fhir/Patient?mothersMaidenName=Abels HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                  |
| ----------- | ------ | ---------------------------------------------------------------------------- |
| MUST        |        | Accept the message with HTTP 200 OK                                          |
| MUST        |        | Include a bundle with exactly 1 patient result.                              |
| MUST        |        | Contain the child patient details                                            |
| MUST        |        | Have an identifier for FHR-051 in system http://ohie.org/test/test           |
| SHOULD      |        | Contain one or more link entries with type seealso pointing to local records |
