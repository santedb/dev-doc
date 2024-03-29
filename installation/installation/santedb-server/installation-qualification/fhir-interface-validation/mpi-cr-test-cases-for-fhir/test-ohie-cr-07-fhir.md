---
description: Full Patient Registration
---

# TEST: OHIE-CR-07-FHIR

This test ensures that the Client Registry can properly store key fields related to patient demographics fields, and faithfully return them on subsequent queries using the fields stored within the CR ensuring that the CR properly supports the PDQm query parameters.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)
* [Integrating the Health Enterprise Patient Demographics Query for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PDQm.pdf)

## Discussion

The IHE PDQm transaction is used in scenarios where demographics fields are used to locate candidate demographics entries to/from the client registry's central store. The Client Registry is expected to:

* Be capable of storing all demographics fields in the registration message within this test
* Perform matching on the provided demographics fields with the fields in its data store
* Apply appropriate modifiers to the search query parameters that allow a client to have control over the nature of matching.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-02](test-ohie-cr-02-fhir.md#pre-conditions-setup) and [TEST: OHIE-CR-06](test-ohie-cr-06-fhir.md) have been run.

### Create ORGs Domain

The ORG domain is registered to support the identifiers given to organizations in the SanteDB instance.&#x20;

```markup
<dataset id="ORG Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE Organization Domain</name>
      <domainName>ORG</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.20</oid>
      <url>http://ohie.org/test/orgs</url>
      <isUnique>true</isUnique>
    </AssigningAuthority>
  </insert>
</dataset>
```

#### Create PROVIDERs Domain

The providers domain is registered to support the identifiers given to practitioners / providers.

In SanteDB this can be seeded with a dataset:&#x20;

```markup
<dataset id="NID Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE Providers Domain</name>
      <domainName>PROVIDERS</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.21</oid>
      <url>http://ohie.org/test/practs</url>
      <isUnique>true</isUnique>
    </AssigningAuthority>
  </insert>
</dataset>
```

## Authenticate as TEST\_HARNESS

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness.

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

## Register Flynn Full Profile

The test harness will register a patient into the client registry which has a complete demographics profile. The patient resource being registered has the following attributes:

* Identifier `FHR-070` in domain `http://ohie.org/test/test`
* Official Name: Dr. (Prefix) Flynn Full (Given) Profile (Surname) III (Suffix)
* Alias: Dr. Profile
* Home Address: Unit 32 (Line) 123 Ontario St. (Line) , Beamsville (City), Lincoln (District), Ontario (State), Canada (Country), L0R2A0 (Postal Code)
* Workplace Phone: +12039203
* Home Email: flynn@ohie.org
* Mobile: +10293829343
* Gender: Male
* Birthdate: 1982-03-02
* Marital Status: Married
* Contact:
  * Insurance Company
  * Name: ACME Insurance Corp.
  * Organization: Organization/ohie-cr-07-10-fhir
* Contact:
  * Relationship: Next of Kin / Contact&#x20;
  * Name: Allison Profile
  * Address: 123 Ontario St. Beamsville, Lincoln, Ontario, Canada L0R2A0
  * Gender: Female
* Communication: EN (Preferred), FR
* General Practitioner: Practitioner/ohie-cr-07-10-fhir
* Managing Organization: Organization/ohie-cr-07-10-fhir-emp

Additionally, the message has registration information for Flynn's insurance provider ACME Insurance, Flynn's Wife Allison Profile, Flynn's Practitioner Dr. Andrew Fudd, and his Managing Organization University Medical Centre.

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-07-10-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-07-10-fhir"
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
      "fullUrl": "http://test.ohie.org/fhir/Bundle/ohie-cr-07-10-fhir",
      "resource": {
        "resourceType": "Bundle",
	   "id": "ohie-cr-07-10-fhir",
        "type": "history",
        "entry": [
          {
            "fullUrl": "http://test.ohie.org/fhir/Organization/ohie-cr-07-10-fhir-acme",
            "resource": {
              "resourceType": "Organization",
              "id": "ohie-cr-07-10-fhir-acme",
              "identifier": [
                {
                  "use": "usual",
                  "system": "http://ohie.org/test/orgs",
                  "value": "FHR-072"
                }
              ],
              "name": "ACME Insurance Providers Corp.",
              "address": [
                {
                  "use": "work",
                  "type": "physical",
                  "text": "321 James St. North Hamilton, Ontario, Canada, L8K5X2",
                  "line": [
                    "321 James St. North"
                  ],
                  "city": "Hamilton",
                  "state": "ON",
                  "postalCode": "L8K5X2",
                  "country": "CA"
                }
              ]
            },
            "request": {
              "method": "POST",
              "url": "Organization/ohie-cr-07-fhir-acme"
            }
          },
          {
            "fullUrl": "http://test.ohie.org/fhir/Organization/ohie-cr-07-fhir-mgr",
            "resource": {
              "resourceType": "Organization",
              "id": "ohie-cr-07-fhir-mgr",
              "identifier": [
                {
                  "use": "usual",
                  "system": "http://ohie.org/test/orgs",
                  "value": "FHR-073"
                }
              ],
              "name": "University Medical Centre"
            },
            "request": {
              "method": "POST",
              "url": "Organization/ohie-cr-07-fhir-mgr"
            }
          },
          {
            "fullUrl": "http://test.ohie.org/fhir/Practitioner/ohie-cr-07-fhir-pract",
            "resource": {
              "resourceType": "Practitioner",
              "id": "ohie-cr-07-fhir-pract",
              "identifier": [
                {
                  "use": "usual",
                  "system": "http://ohie.org/test/practs",
                  "value": "FHR-074"
                }
              ],
              "name": [
                {
                  "use": "usual",
                  "family": "Profile",
                  "prefix": [ "Dr" ]
                }
              ],
              "telecom": [
                {
                  "system": "phone",
                  "value": "+19054854858",
                  "use": "mobile"
                }
              ],
              "address": [
                {
                  "use": "work",
                  "type": "both",
                  "text": "Unit 493, 5 West 9th Ave. Grimsby, Ontario, Canada",
                  "line": [
                    "5 West 9th Ave.",
                    "Unit 493"
                  ],
                  "city": "Grimsby",
                  "state": "ON",
                  "postalCode": "L4N3N4",
                  "country": "CA"
                }
              ]
            },
            "request": {
              "method": "POST",
              "url": "Practitioner/ohie-cr-07-fhir-pract"
            }
          },
          {
            "fullUrl": "http://test.ohie.org/fhir/Patient/ohie-cr-07-10-fhir-flyn",
            "resource": {
              "resourceType": "Patient",
              "id": "ohie-cr-07-10-fhir-flyn",
              "active": true,
              "identifier": [
                {
                  "use": "official",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-070"
                }
              ],
              "name": [
                {
                  "use": "official",
                  "family": "Profile",
                  "given": [
                    "Flynn",
                    "Full"
                  ],
                  "prefix": [ "Dr" ],
                  "suffix": [ "III" ]
                },
                {
                  "use": "usual",
                  "family": "Profile",
                  "prefix": [ "Dr" ]
                }
              ],
              "address": [
                {
                  "use": "home",
                  "type": "both",
                  "text": "123 Ontario St. Beamsville, Lincoln County, Ontario, Canada, L0R2A0",
                  "line": [
                    "123 Ontario St",
                    "Unit 32"
                  ],
                  "city": "Beamsville",
                  "district": "Lincoln County",
                  "state": "ON",
                  "postalCode": "L0R2A0",
                  "country": "CA"
                }
              ],
              "telecom": [
                {
                  "system": "phone",
                  "value": "+12039203099",
                  "use": "work"
                },
                {
                  "system": "phone",
                  "value": "+10293829343",
                  "use": "mobile"
                },
                {
                  "system": "email",
                  "value": "flynn@ohie.org",
                  "use": "home"
                }
              ],
              "gender": "male",
              "birthDate": "1982-03-02",
              "maritalStatus": {
                "coding": [
                  {
                    "system": "http://terminology.hl7.org/CodeSystem/v3-MaritalStatus",
                    "code": "M",
                    "display": "Married"
                  }
                ]
              },
              "multipleBirthBoolean": true,
              "contact": [
                {
                  "relationship": [
                    {
                      "coding": [
                        {
                          "system": "http://terminology.hl7.org/CodeSystem/v2-0131",
                          "code": "C"
                        }
                      ]
                    },
                    {
                      "coding": [
                        {
                          "system": "http://terminology.hl7.org/CodeSystem/v2-0131",
                          "code": "N"
                        }
                      ]
                    }
                  ],
                  "name": {
                    "use": "usual",
                    "family": "Profile",
                    "given": [
                      "Allison"
                    ]
                  },
                  "address": {
                    "use": "home",
                    "type": "both",
                    "text": "123 Ontario St. Beamsville, Lincoln County, Ontario, Canada, L0R2A0",
                    "line": [
                      "123 Ontario St",
                      "Unit 32"
                    ],
                    "city": "Beamsville",
                    "district": "Lincoln County",
                    "state": "ON",
                    "postalCode": "L0R2A0",
                    "country": "CA"
                  },
                  "telecom": [
                    {
                      "system": "phone",
                      "value": "+13049303940",
                      "use": "mobile"
                    }
                  ]
                },
                {
                  "relationship": [
                    {
                      "coding": [
                        {
                          "system": "http://terminology.hl7.org/CodeSystem/v2-0131",
                          "code": "I"
                        }
                      ]
                    }
                  ],
                  "organization": {
                    "reference": "http://test.ohie.org/fhir/Organization/ohie-cr-07-10-fhir-acme",
                    "display": "ACME Insurance Corp."
                  }
                }
              ],
              "communication": [
                {
                  "language": {
                    "coding": [
                      {
                        "system": "urn:ietf:bcp:47",
                        "code": "en",
                        "display": "English"
                      }
                    ]
                  },
                  "preferred": true
                },
                {
                  "language": {
                    "coding": [
                      {
                        "system": "urn:ietf:bcp:47",
                        "code": "fr",
                        "display": "French"
                      }
                    ]
                  },
                  "preferred": false
                }
              ],
              "generalPractitioner": {
                "reference": "http://test.ohie.org/fhir/Practitioner/ohie-cr-07-fhir-pract",
                "display": "Dr. Andrew Fudd"
              },
              "managingOrganization": {
                "reference": "http://test.ohie.org/fhir/Organization/ohie-cr-07-fhir-mgr",
                "display": "University Medical Centre"
              }
            },
            "request": {
              "method": "POST",
              "url": "Patient/ohie-cr-01-10-fhir-flyn"
            }
          },
          {
            "fullUrl": "http://test.ohie.org/fhir/RelatedPerson/ohie-cr-07-10-fhir-wife",
            "resource": {
              "resourceType": "RelatedPerson",
              "id": "ohie-cr-07-10-fhir-wife",
              "identifier": [
                {
                  "use": "usual",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-071"
                },
                {
                  "use": "usual",
                  "system": "http://ohie.org/test/nid",
                  "value": "NID071"
                }
              ],
              "patient": {
                "reference": "http://test.ohie.org/fhir/Patient/ohie-cr-07-10-fhir-flyn"
              },
              "relationship": [
                {
                  "coding": [
                    {
                      "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
                      "code": "WIFE"
                    }
                  ]
                }
              ],
              "name": {
                "use": "usual",
                "family": "Profile",
                "given": [
                  "Allison"
                ]
              },
              "address": [
                {
                  "use": "home",
                  "type": "both",
                  "text": "123 Ontario St. Beamsville, Lincoln County, Ontario, Canada, L0R2A0",
                  "line": [
                    "123 Ontario St",
                    "Unit 32"
                  ],
                  "city": "Beamsville",
                  "district": "Lincoln County",
                  "state": "ON",
                  "postalCode": "L0R2A0",
                  "country": "CA"
                }
              ],
              "telecom": [
                {
                  "system": "phone",
                  "value": "+13049303940",
                  "use": "mobile"
                }
              ],
              "birthDate": "1985-05-10",
              "gender": "female"
            },
            "request": {
              "method": "POST",
              "url": "RelatedPerson/ohie-cr-07-10-fhir-wife"
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
| SHOULD      |           | Include a link to the master identity with code refer          |

## Query By Patient Identifier

The test harness issues a query for patient demographics using the Patient's NID identifier

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-070 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                                                              |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| MUST        |        | Return a bundle in JSON format                                                                                           |
| MUST        |        | Return HTTP code of 200                                                                                                  |
| MUST        |        | Contain a bundle with exactly 1 result                                                                                   |
| MUST        |        | Match full demographics details outlined in Registration step                                                            |
| SHOULD      |        | <p>Return the master identity and have links to the local identities</p><p>in one or more <code>link</code> elements</p> |

## Retrieve Full Patient Profile

The test harness issues a query for patient demographics using the Patient's NID identifier and instructs the inclusion of all data

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-070&_include=Organization%3AmanagingOrganization&_revinclude=RelatedPerson%3Apatient HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                                                                                                              |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| MUST        |        | Return a bundle in JSON format                                                                                           |
| MUST        |        | Return HTTP code of 200                                                                                                  |
| MUST        |        | Contain a bundle with exactly 1 result                                                                                   |
| MUST        |        | Match full demographics details outlined in Registration step                                                            |
| SHOULD      |        | <p>Return the master identity and have links to the local identities</p><p>in one or more <code>link</code> elements</p> |

## Query By Patient Name

The test harness issues a query for patient demographics using the Patient's family and given names.

```http
GET http://localhost:8080/fhir/Patient?family=Profile&given=Flynn HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

**Alternate**: The test harness issues a query for patient using an exact modifier&#x20;

```http
GET http://sut:8080/fhir/Patient?family=Profile&given%3Aexact=Flynn HTTP/1.1
Accept: application/fhir+json
Authorization: bearer XXXXYYYXXYX
```

### Expected Behaviour

| Requirement | Option | Description                                                                                                              |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| MUST        |        | Return a bundle in JSON format                                                                                           |
| MUST        |        | Return HTTP code of 200 Created                                                                                          |
| MUST        |        | Contain a bundle with exactly 1 result                                                                                   |
| MUST        |        | Match full demographics details outlined in Registration step                                                            |
| SHOULD      |        | <p>Return the master identity and have links to the local identities</p><p>in one or more <code>link</code> elements</p> |

## Query By Approximate Birthdate

The test harness sends a query to the client registry requests results based on a given birth date.

```http
GET http://localhost:8080/fhir/Patient?birthdate=ap1982 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                                                                                                              |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| MUST        |        | Return a bundle in JSON format                                                                                           |
| MUST        |        | Return HTTP code of 200                                                                                                  |
| MUST        |        | Contain a result within the bundle with identifier matching FHR-070                                                      |
| MUST        |        | Patient must match demographics details outlined in Registration step                                                    |
| SHOULD      |        | <p>Return the master identity and have links to the local identities</p><p>in one or more <code>link</code> elements</p> |

## Query By Combination of Parameters&#x20;

{% hint style="info" %}
This test is equivalent to OHIE-CR-15
{% endhint %}

The test harness sends a query to the client registry requests results based on a given birth date, family name, and given name .

### Query By Name and Date Of Birth

```http
GET http://localhost:8080/fhir/Patient?family=Profile&given=Flynn&birthdate=ap1982 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Query By Gender and Family Name

```http
GET http://localhost:8080/fhir/Patient?family=Profile&gender=male HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Query By Gender and Date Of Birth

```http
GET http://localhost:8080/fhir/Patient?birthdate=1982-03-02&gender=male HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                                                                                                              |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| MUST        |        | Return a bundle in JSON format                                                                                           |
| MUST        |        | Return HTTP code of 200                                                                                                  |
| MUST        |        | Contain exactly 1 result within the bundle with identifier matching FHR-070                                              |
| MUST        |        | Patient must match demographics details outlined in Registration step                                                    |
| SHOULD      |        | <p>Return the master identity and have links to the local identities</p><p>in one or more <code>link</code> elements</p> |

## No-Result Queries

This test step ensures that the demographics query provider behaves appropriately when no results are found. The test harness sends a query for demographics which results in no matches:

```http
GET http://localhost:8080/fhir/Patient?given=Profile&gender=other HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                            |
| ----------- | ------ | -------------------------------------- |
| MUST        |        | Return a bundle in JSON format         |
| MUST        |        | Return HTTP code of 200                |
| MUST        |        | Contain exactly 0 entry elements       |
| MUST        |        | Contain a `total` element with value 0 |

## Restricting Domains Returned

This step ensures that the PDQm provider implements the behaviour described in `3.78.4.1.2.4`. The test harness sends a PDQm query and requests domains returned, and ensures that the SUT removes non-compatible domains.

```http
GET http://localhost:8080/fhir/RelatedPerson?identifier=http%3A%2F%2Fohie.org%2Ftest%2Fnid%7CNID071 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                                                          |
| ----------- | ------ | -------------------------------------------------------------------- |
| MUST        |        | Return a bundle in JSON format                                       |
| MUST        |        | Return HTTP code of 200                                              |
| MUST        |        | Contain exactly 1 entry element                                      |
| MUST        |        | Entry element must contain exactly 1 identifier with value `FHR-070` |
| MUST        |        | Entry element must not contain the TEST domain value of `FHR-071`    |
| MUST        |        | Contain a `total` element with value 1                               |

