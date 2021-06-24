---
description: Full Patient Registration
---

# TEST: OHIE-CR-07-FHIR

This test ensures that the Client Registry can properly store key fields related to patient demographics fields, and faithfully return them on subsequent queries using the fields stored within the CR.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)
* [Integrating the Health Enterprise Patient Demographics Query for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PIXm.pdf)

## Discussion

The IHE PDQm transaction is used in scenarios where demographics fields are used to locate candidate demographics entries to/from the client registry's central store. The Client Registry is expected to:

* Be capable of storing all demographics fields in the registration message within this test
* Perform matching on the provided demographics fields with the fields in its data store
* Apply appropriate modifiers to the search query parameters that allow a client to have control over the nature of matching.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-02](test-ohie-cr-02-fhir.md#pre-conditions-setup) have been run.

### Create ORGs Domain

The ORG domain is registered to support the identifiers given to organizations in the SanteDB instance. 

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

In SanteDB this can be seeded with a dataset: 

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
POST http://sut:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: sut:8080
Content-Length: 112

grant_type=client_credentials&scope=*&client_id=TEST_HARNESS&client_secret=TEST_HARNESS
```

## Register Flynn Full Profile

The test harness will register a patient into the client registry which has a complete demographics profile. The patient resource being registered has the following attributes:

* Identifier `FHR-070` in domain `http://ohie.org/test/test`
* Official Name: Dr. \(Prefix\) Flynn Full \(Given\) Profile \(Surname\) III \(Suffix\)
* Alias: Dr. Profile
* Home Address: Unit 32 \(Line\) 123 Ontario St. \(Line\) , Beamsville \(City\), Lincoln \(District\), Ontario \(State\), Canada \(Country\), L0R2A0 \(Postal Code\)
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
  * Relationship: Next of Kin / Contact 
  * Name: Allison Profile
  * Address: 123 Ontario St. Beamsville, Lincoln, Ontario, Canada L0R2A0
  * Gender: Female
* Communication: EN \(Preferred\), FR
* General Practitioner: Practitioner/ohie-cr-07-10-fhir
* Managing Organization: Organization/ohie-cr-07-10-fhir-emp

Additionally, the message has registration information for Flynn's insurance provider ACME Insurance, Flynn's Wife Allison Profile, Flynn's Practitioner Dr. Andrew Fudd, and his Managing Organization University Medical Centre.

```javascript
{
  "resourceType": "Bundle",
  "type": "history",
  "entry": [
    {
      "fullUrl": "Patient/ohie-cr-07-10-fhir-flyn",
      "resource": {
        "resourceType": "Patient",
        "id": "ohie-cr-07-10-fhir-flyn",
        "active": true,
        "identifier": [
          {
            "use": "official",
            "system": "http://ohie.org/test/test",
            "value": "FHR-070"
          },
          {
            "use": "official",
            "system": "http://ohie.org/test/nid",
            "value": "NID070"
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
              "reference": "Organization/ohie-cr-07-fhir-acme",
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
          "reference": "Practitioner/ohie-cr-07-fhir-pract",
          "display": "Dr. Andrew Fudd"
        },
        "managingOrganization": {
          "reference": "Organization/ohie-cr-07-fhir-mgr",
          "display": "University Medical Centre"
        }
      },
      "request": {
        "method": "POST",
        "url": "Patient/ohie-cr-01-10-fhir-flyn"
      }
    },
    {
      "fullUrl": "RelatedPerson/ohie-cr-07-10-fhir-wife",
      "resource": {
        "resourceType": "RelatedPerson",
        "id": "ohie-cr-07-10-fhir-wife",
        "identifier": [
          {
            "use": "official",
            "system": "http://ohie.org/test/test",
            "value": "FHR-071"
          }
        ],
        "patient": {
          "reference": "Patient/ohie-cr-07-10-fhir-flyn"
        },
        "relationship": [
          {
            "coding": [
              {
                "system": "http://terminology.hl7.org/CodeSystem/v3-RoleCode",
                "code": "WIFE"
              }
            ]
          },
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
    },
    {
      "fullUrl": "Organization/ohie-cr-07-fhir-acme",
      "resource": {
        "resourceType": "Organization",
        "id": "ohie-cr-07-fhir-acme",
        "identifier": [
          {
            "use": "normal",
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
      "fullUrl": "Organization/ohie-cr-07-fhir-mgr",
      "resource": {
        "resourceType": "Organization",
        "id": "ohie-cr-07-fhir-mgr",
        "identifier": [
          {
            "use": "normal",
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
      "fullUrl": "Parctitioner/ohie-cr-07-fhir-pract",
      "resource": {
        "resourceType": "Practitioner",
        "id": "ohie-cr-07-fhir-pract",
        "identifier": [
          {
            "use": "normal",
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
        "url": "Organization/ohie-cr-07-fhir-pract"
      }
    }
  ]
}
```



