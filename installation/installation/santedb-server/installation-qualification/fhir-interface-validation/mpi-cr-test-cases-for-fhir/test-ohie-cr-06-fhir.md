---
description: Patient Identity Cross Referencing
---

# TEST: OHIE-CR-06-FHIR

This test ensures that the receiver registers patients in two different identity domains (`TEST_A`and `TEST_B` ) and ensures that the receiver can appropriately cross reference the two identifiers in the identity domains using the IHE Patient Identity Cross Referencing (PIXm) transactions.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)
* [Integrating the Health Enterprise Patient Identity Cross Reference for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PIXm.pdf)

## Discussion

The IHE PIXm transaction is used in scenarios where only cross-referenced identities are disclosed to callers. The transaction is implemented as an operation on the Client Registry and is invoked returning a collection of parameters which represent the cross referenced identities and no further patient information.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-04](test-ohie-cr-04-fhir.md#pre-conditions-setup) have been run.

### Create NID Domain

The NID domain is a sample domain which is being used to simulate a globally assignable national identifier (such as a citizen card, etc.) which can be used by the receiver to eliminate fuzzy matching from this test case.&#x20;

```markup
<dataset id="NID Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE NID TEST Domain</name>
      <domainName>NID</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.9</oid>
      <url>http://ohie.org/test/nid</url>
      <isUnique>true</isUnique>
    </AssigningAuthority>
  </insert>
</dataset>
```

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

## Execute PIXm Query for Non-Existent Patient in TEST\_A

The test harness sends an IHE PIXm query for a patient with identifier FHIRA-8767 to the receiver.

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest_a%7CFHRA-060 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description                                         |
| ----------- | ------ | --------------------------------------------------- |
| MUST        |        | Return HTTP code of 404 NOT FOUND                   |
| MUST        |        | Include an OperationOutcome entry in the response   |
| MUST        |        | Include have a detail with issue type not-found     |
| SHOULD      |        | Indicate the the identifier pair which is not found |

## Register New Patient Identity in TEST\_A

The test harness sends an authenticated request to create a new patient with a new identifier in TEST\_A domain. Patient details:

* Identifier `FHRA-061` in `http://ohie.org/test/test_a` with use `official`
* Identifier `NID061` in `http://ohie.org/test/nid`&#x20;
* Name: JIM SMITH
* Gender: Male
* DOB: 1984-05-25

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-06-20-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness_b"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-06-10-fhir"
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
      "fullUrl": "Bundle/ohie-cr-06-10-fhir",
      "resource": {
        "resourceType": "Bundle",
        "type": "history",
        "entry": [
          {
            "fullUrl": "Patient/ohie-cr-06-10-fhir",
            "resource": {
		    "resourceType": "Patient",
		    "id": "ohie-cr-06-10-fhir",
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
		        "value": "FHRA-061",
		        "assigner": {
		          "display": "Test Harness A Patient Identity"
		        }
		      },
		      {
		        "use":"usual",
		        "system": "http://ohie.org/test/nid",
		        "value":"NID061"
		      }
		    ],
		    "name": [
		      {
		        "use": "official",
		        "family": "SMITH",
		        "given": [
		          "JIM"
		        ]
		      }
		    ],
		    "gender": "male",
		    "birthDate": "1984-05-25",
		  },
            "request": {
              "method": "POST",
              "url": "Patient/ohie-cr-06-10-fhir"
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

## Execute PIXm Query Patient in TEST\_A

The test harness sends an IHE PIXm query for a patient with identifier FHRA-061 to the receiver.

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest_a%7CFHRA-061 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                                                                   |
| ----------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| MUST        |        | Return HTTP code of 200 OK                                                                                                    |
| MUST        |        | Include a Parameters resource in the response                                                                                 |
| MUST        |        | <p>Have two parameters carrying the identifier in TEST_A and NID </p><p>with parameter name of targetIdentifier</p>           |
| MUST        |        | <p>Include a parameter with name targetId which has a resource link</p><p>to the created resource from the previous step.</p> |

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

* Identifier `FHRB-062` in `http://ohie.org/test/test_b` with use `official`
* Identifier `NID061` in `http://ohie.org/test/nid`&#x20;
* Name: JIM SMITH
* Gender: Male

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-06-20-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness_b"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-06-20-fhir"
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
      "fullUrl": "Bundle/ohie-cr-06-20-fhir",
      "resource": {
        "resourceType": "Bundle",
        "type": "history",
        "entry": [
          {
            "fullUrl": "Patient/ohie-cr-06-20-fhir",
            "resource": {
		    "resourceType": "Patient",
		    "id": "ohie-cr-06-20-fhir",
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
		        "value": "FHRB-062",
		        "assigner": {
		          "display": "Test Harness B Patient Identity"
		        }
		      },
		      {
		        "use":"usual",
		        "system": "http://ohie.org/test/nid",
		        "value":"NID061"
		      }
		    ],
		    "name": [
		      {
		        "use": "official",
		        "family": "SMITH",
		        "given": [
		          "JIM"
		        ]
		      }
		    ],
		    "gender": "male"
		  },
            "request": {
              "method": "POST",
              "url": "Patient/ohie-cr-06-20-fhir"
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

## Execute PIXm Query Patient using NID for TEST\_A

The test harness sends an IHE PIXm query for a patient with identifier NID061 to the receiver and explicitly requests a resolve to TEST\_A.

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Fnid%7CNID061&targetSystem=http%3A%2F%2Fohie.org%2Ftest%2Ftest_a HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                                                                   |
| ----------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| MUST        |        | Return HTTP code of 200 OK                                                                                                    |
| MUST        |        | Include a Parameters resource in the response                                                                                 |
| MUST        |        | Have one parameter carrying the identifier FHRA-061 in `TEST_A`                                                               |
| MUST        |        | <p>Include a parameter with name targetId which has a resource link</p><p>to the created resource from the previous step.</p> |

## Execute PIXm Query Patient using TEST\_B for TEST\_X

The test harness sends an IHE PIXm query for a patient with identifier FHRB-062 to the receiver asking for identities in TEST\_X.

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest_b%7CFHRB-062&targetSystem=http%3A%2F%2Fohie.org%2Ftest%2Ftest_x HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                      |
| ----------- | ------ | -------------------------------------------------------------------------------- |
| MUST        |        | Return HTTP code of 403 FORBIDDEN                                                |
| MUST        |        | Include an OperationOutcome resource in the response                             |
| MUST        |        | Carry an issue type code-invalid                                                 |
| SHOULD      |        | Include a description that indicates the domain which caused the error condition |
