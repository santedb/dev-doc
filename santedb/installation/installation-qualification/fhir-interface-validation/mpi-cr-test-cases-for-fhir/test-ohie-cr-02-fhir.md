---
description: Patient Identity Feed - Resolve Identity Domains
---

# TEST: OHIE-CR-02-FHIR

This test is a modified version of OHIE-CR-02 test case for HL7v2. Whereas the HL7v2 PIX behavior is intended to map missing identity domains to an authority, this test ensures that the solution can map between URL and OID identity systems.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)

## Discussion

Jurisdictional deployments often use a heterogenous mixture of standards and software. Some software, such as those using HL7v2 or HL7v3/CDA may use OIDs and/or named identity domains for patient identification, whereas FHIR based systems may prefer URLs. These tests ensure that the SanteMPI solution maintains a consistent mapping between OID based identity domains and URL based identity domains.

## Pre-Conditions / Setup

### Create TEST Domain

Create an AssigningAuthority domain which has the following attributes:

* URL of http://ohie.org/test/test
* OID of 1.3.6.1.4.1.52820.3.72.5.9.1
* Device TEST-HARNESS with authoritative source for identifiers

#### SanteMPI Seed Data

```markup
<dataset id="Test Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <insert skipIfError="false" skipIfExists="true">
    <SecurityApplication xmlns="http://santedb.org/model">
      <id>F0FC4322-948D-4986-A06C-DA603A77EDDE</id>
      <!-- Secret: TEST_HARNESS -->
      <applicationSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</applicationSecret>
      <name>TEST_HARNESS</name>
    </SecurityApplication>
  </insert>
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE TEST Domain</name>
      <domainName>TEST_FHIR</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.1</oid>
      <url>http://ohie.org/test/test</url>
      <isUnique>true</isUnique>
      <assigningApplication>F0FC4322-948D-4986-A06C-DA603A77EDDE</assigningApplication>
    </AssigningAuthority>
  </insert>
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

## Register Olly Oid

The test harness registers a patient using the OID for the TEST domain with the following additional data:

* Name: Olly Oid
* Gender: male
* Identifier: FHR-020 , system: urn:oid:1.3.6.1.4.1.52820.3.72.5.9.1

```javascript
{
  "resourceType": "Patient",
  "id": "ohie-cr-02-10-fhir",
  "active": true,
  "identifier": [
    {
      "system": "urn:oid:2.16.840.1.113883.3.72.5.9.1",
      "value": "FHR-020"
    }
  ],
  "name": [
    {
      "use": "official",
      "family": "OID",
      "given": [
        "OLLY"
      ]
    }
  ],
  "gender": "male",
  "birthDate": "1983-02-05"
}
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP response code 201 Created |
| SHOULD |  | Include created patient object in response |
| SHOULD |  | Indicate the identifier of the created patient with URL |
| SHOULD |  | Contain a link to the local record created |

## Query for Olly Oid using Url

The test harness executes a query against the receiver using the URL version of the TEST domain

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-020&_format=application%2Ffhir%2Bjson HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER xxxxxxx
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Accept the message with HTTP 200 OK |
| MUST |  | Include a bundle with exactly 1 patient result |
| MUST |  | Contain a patient for Olly Oid |
| MUST |  | Have an identifier for FHR-020 in system http://ohie.org/test/test |
| SHOULD |  | Contain one or more link entries with type seealso |

## Register Uma Url

The test harness registers a patient using the URL representation of the system for the TEST domain:

* Name: Uma Url
* Gender: female
* Identifier: FHR-021 , system: http://ohie.org/test/test

```javascript
{
			  "resourceType": "Patient",
			  "id": "ohie-cr-02-30-fhir",
			  "active": true,
			  "identifier": [
			    {
			      "system": "http://ohie.org/test/test",
			      "value": "FHR-021"
			    }
			  ],
			  "name": [
			    {
			      "use": "official",
			      "family": "URL",
			      "given": [
			        "UMA"
			      ]
			    }
			  ],
			  "gender": "female",
			  "birthDate": "1990-03-09"
			}
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP response code 201 Created |
| SHOULD |  | Include created patient object in response |
| SHOULD |  | Indicate the identifier of the created patient with URL |
| SHOULD |  | Contain a link to the local record created |

## Query for Uma Url using Oid

The test harness executes a query against the receiver using the OID version of the TEST domain

```http
GET http://localhost:8080/fhir/Patient?identifier=urn%3Aoid%3A2.16.840.1.113883.3.72.5.9.1%7CFHR-021&_format=application%2Ffhir%2Bjson HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER xxxxxxx
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Accept the message with HTTP 200 OK |
| MUST |  | Include a bundle with exactly 1 patient result |
| MUST |  | Contain a patient for Uma Url |
| MUST |  | Have an identifier for FHR-021 in system http://ohie.org/test/test |
| SHOULD |  | Contain one or more link entries with type seealso |



