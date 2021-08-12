---
description: Patient Identity Feed - Blocks Inappropriate Assigner
---

# TEST: OHIE-CR-04-FHIR

This test ensures that an assigner cannot inappropriately attempt to assign an authoritative \(official\) identity for a domain which it does not have appropriate authority to do so. 

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)

## Discussion

SanteMPI provides mechanisms for two types of identity domains:

* Open Identity Domains - Whereby any caller from any source can freely assign new identifiers in that domain \(for example: in use cases where the DLN authority is not directly integrated to the MPI you can allow any EMR to assign / register a DLN\)
* Protected Identity Domains - Whereby only the registered source for identities in that domain can assign new identifiers and be authoritative. For example, only the national health insurance provider may notify the MPI/CR about new health insurance numbers, or only Hospital A can notify the CR about official identifiers form Hospital A.

When protected identity domains are used, other sources may provide identifiers in protected domains, however they are treated as informative rather than "official" authoritative sources. This information can be taken into consideration when weighing a candidate match. Additionally, non-authoritative sources can link their own records with existing identifiers in a protected identity domain.

## Pre-Conditions / Setup

### Create TEST\_A Domain

Create an AssigningAuthority domain which has the following attributes:

* URL of http://ohie.org/test/test\_a
* OID of 1.3.6.1.4.1.52820.3.72.5.9.2
* Device TEST-HARNESS-A with authoritative source for identifiers

#### SanteMPI Seed Data

```markup
<dataset id="Test Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <insert skipIfError="false" skipIfExists="true">
    <SecurityApplication xmlns="http://santedb.org/model">
      <id>DE5BEC1E-8C41-4FF1-8E65-A39AC1DDAE60</id>
      <!-- Secret: TEST_HARNESS -->
      <applicationSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</applicationSecret>
      <name>TEST_HARNESS_FHIR_A</name>
    </SecurityApplication>
  </insert>
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE TEST Domain A</name>
      <domainName>TEST_A</domainName>
      <oid>1.3.6.1.4.1.52820.3.72.5.9.2</oid>
      <url>http://ohie.org/test/test_a</url>
      <isUnique>true</isUnique>
      <assigningApplication>DE5BEC1E-8C41-4FF1-8E65-A39AC1DDAE60</assigningApplication>
    </AssigningAuthority>
  </insert>
```

### Create TEST\_B Domain

Create an AssigningAuthority domain which has the following attributes:

* URL of http://ohie.org/test/test\_b
* OID of 1.3.6.1.4.1.52820.3.72.5.9.3
* Device TEST-HARNESS-B with authoritative source for identifiers

#### SanteMPI Seed Data

```markup
<dataset id="Test Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <insert skipIfError="false" skipIfExists="true">
    <SecurityApplication xmlns="http://santedb.org/model">
      <id>58275680-5129-4832-9668-131F76E8DFB6</id>
      <!-- Secret: TEST_HARNESS -->
      <applicationSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</applicationSecret>
      <name>TEST_HARNESS_FHIR_B</name>
    </SecurityApplication>
  </insert>
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE TEST Domain B</name>
      <domainName>TEST_B</domainName>
      <oid>1.3.6.1.4.1.52820.3.72.5.9.3</oid>
      <url>http://ohie.org/test/test_b</url>
      <isUnique>true</isUnique>
      <assigningApplication>58275680-5129-4832-9668-131F76E8DFB6</assigningApplication>
    </AssigningAuthority>
  </insert>
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

## Register New Patient Identity in TEST\_A

The test harness sends an authenticated request to create a new patient with a new identifier in TEST\_A domain. Patient details:

* Identifier `FHRA-040` in `http://ohie.org/test/test_a` with use `official`
* Name: JENNIFER JONES
* Gender: Female
* DOB: 1984-01-25

{% hint style="info" %}
The patient is being sent from a source with the expectation that the information is scoped from the worldview of the sender. So the sender may use an MRN or Patient Internal Identifier \(PI\) as the "official" identifier for the patient in its own world, which may \(or may not\) match the view of the patient from the jurisdictional worldview.
{% endhint %}

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-04-10-fhir",
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
        "value": "FHRA-040",
        "assigner": {
          "display": "Test Harness A Patient Identity"
        }
      }
    ],
    "name": [
      {
        "use": "official",
        "family": "JONES",
        "given": [
          "JENNIFER"
        ]
      }
    ],
    "gender": "female",
    "birthDate": "1984-01-25",
  }
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP code of 201 Created |
| SHOULD | PMIR Only | Include an OperationOutcome entry in the response |
| SHOULD |  | Include a Patient entry in response containing created patient |
| SHOULD |  | Include a link to the master identity with code refer  |

## Validate Patient Created

The test harness executes a query against the receiver to ensure the record was created domain

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest_a%7CFHRA-040&_format=application%2Ffhir%2Bjson HTTP/1.1
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
| MUST |  | Contain a patient for Jennifer Jones |
| MUST |  | Have an identifier for FHRA-040 in system http://ohie.org/test/test\_a |
| SHOULD |  | Contain one or more link entries with type seealso pointing to local records |

## Authenticate as TEST\_HARNESS\_FHIR\_B

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness-b account.

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

## Attempt to Register New Patient Identity in TEST\_A

The test harness sends a registration message to the receiver, attempting to incorrectly register a new official identifier in the TEST\_A domain \(an identity domain for which it does not have authority to assign new identities\).

* Identifier `FHRB-041` in `http://ohie.org/test/test_b` with use `offical`
* Name: JENNIFER DOE
* Gender: Female
* DOB: 1989-01-25

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-04-20-fhir",
    "active": true,
    "identifier": [
      {
        "use": "official",
        "type": {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
              "code": "MR"
            }
          ]
        },
        "system": "http://ohie.org/test/test_a",
        "value": "FHRA-041",
        "assigner": {
          "display": "Test Harness A Patient Identity"
        }
      }
    ],
    "name": [
      {
        "use": "official",
        "family": "DOE",
        "given": [
          "JENNIFER"
        ]
      }
    ],
    "gender": "female",
    "birthDate": "1989-01-25",
  }
```

### Expected Behaviour \(Option 1 - Rejection / Strict\)

If the receiver is behaving in a strict mode \(i.e. emulating the behavior from HL7v2\), then.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Requirement</th>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left">PMIR Only</td>
      <td style="text-align:left">Return MessageHeader with response.code = fatal-error</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return HTTP code in the 400 series</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Include an OperationOutcome entry in the response indicating sender</p>
        <p>does not have authority to issue new identities in the TEST_A domain.</p>
      </td>
    </tr>
  </tbody>
</table>

### Expected Behavior \(Option 2 - Flag as Informative\)

If the receiver is operating in a mode that is lenient for identity domains, it should process the message and flag the identifier as informative.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Requirement</th>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left">PMIR Only</td>
      <td style="text-align:left">Return MessageHeader with response.code = ok</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return HTTP code in the 201 Created</td>
    </tr>
    <tr>
      <td style="text-align:left">SHOULD</td>
      <td style="text-align:left">PMIR Only</td>
      <td style="text-align:left">
        <p>Include an OperationOutcome entry in the response indicating sender</p>
        <p>does not have authority to issue new identities in the TEST_A domain
          <br
          />and code official was changed to usual/secondary.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SHOULD</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Return the created patient with the identifier FHRB-041 with use</p>
        <p>set to usual/secondary and/or an extension indicating the identifier</p>
        <p>is informative.</p>
      </td>
    </tr>
  </tbody>
</table>

## Attempt to Register New Patient Identity in TEST\_B with existing Identity in TEST\_A

The test harness sends a registration for a new patient in its own identity domain where the patient has an existing identity in another protected domain.

{% hint style="info" %}
This mimics a use case where TEST B is registering a patient on a referral that came from TEST A or where TEST A is, in fact, a health insurance number or some other identifier domain from an official source.
{% endhint %}

* Identifier `FHRB-042` in `http://ohie.org/test/test_b` with use `official`
* Identifier `FHRA-040` in `http://ohie.org/test/test_a` with use `usual`
* Name: JENNIFER JONES
* Gender: Female
* DOB: 1984-01-25

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-04-30-fhir",
    "active": true,
    "identifier": [
      {
        "use": "usual",
        "type": {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
              "code": "PT"
            }
          ]
        },
        "system": "http://ohie.org/test/test_a",
        "value": "FHRA-040",
        "assigner": {
          "display": "Test Harness A Patient Identity"
        }
      },
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
        "value": "FHRB-042",
        "assigner": {
          "display": "Test Harness B Patient Identity"
        }
      }
    ],
    "name": [
      {
        "use": "official",
        "family": "JONES",
        "given": [
          "JENNIFER"
        ]
      }
    ],
    "gender": "female",
    "birthDate": "1984-01-25",
  }
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP code of 201 Created |
| SHOULD | PMIR Only | Include an OperationOutcome entry in the response |
| SHOULD |  | Include a Patient entry in response containing created patient |
| SHOULD |  | Include a link to the master identity with code refer |

## Validate Patient Created / Linked

The test harness executes a query against the receiver to ensure the record was created domain

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest_b%7CFHRB-042&_format=application%2Ffhir%2Bjson HTTP/1.1
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
| MUST |  | Contain a patient for Jennifer Jones |
| MUST |  | Have an identifier for FHRB-042 in system http://ohie.org/test/test\_b |
| MUST |  | Have identifier for FHRA-040 in system http://ohie.org/test/test\_a |
| SHOULD |  | Contain a link entry with type seealso pointing to local records from TEST HARNESS A |
| SHOULD |  | Contain a link entry with type seealso pointing to local record from TEST HARNESS B |



