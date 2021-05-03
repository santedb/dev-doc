# TEST: OHIE-CR-05-FHIR

This test ensures that the receiver can create a record with minimally useful information linked to another person/patient. This is often useful when registering an infant demographic record where only date of birth, gender and mother's information is known.

{% hint style="info" %}
This test is a combination of TEST-OHIE-CR05 and TEST-OHIE-CR07 from the HL7v2 test suite.
{% endhint %}

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)

## Discussion

A master patient index/client registry is often tasked with the storage of partial registration records and/or records which are only identifiable by their mother's information. 

Whereas this information can be registered in one message in HL7v2 \(using mother's name and mother's identifier\), this test requires the use of either:

* A FHIR transaction bundle to register a related person \(the mother\) and patient
* Two FHIR operations to register the patient and the related person \(the mother\)
* A PMIR message with the related person \(the mother\) and patient.

### FHIR Representation of Mother/Child Relationship

SanteMPI supports robust relationships between entities which cannot be easily expressed in FHIR. For example, there may be use cases where the mother is a patient \(via delivery\) at a hospital and the child is also a patient \(receiving care at a NICU\). Unfortunately, this type of relationship in FHIR is represented as the following structure:

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

* The three resources are submitted as part of an entire bundle \(such as a transaction bundle or PMIR operation\)
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
POST http://sut:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: sut:8080
Content-Length: 112

grant_type=client_credentials&scope=*&client_id=TEST_HARNESS_FHIR&client_secret=TEST_HARNESS
```

## Register Mother / Child Demographics in Transaction Bundle

The test harness sends an authenticated request to create a child record with a mother's demographics as a simple related person.

* Identifier FHR-4956 in http://ohie.org/test/test with use official
* Name: WIN MINH
* Gender: Male
* DOB: 2017-04-03

The mother is a simple Related Person with name SU MYAT LWIN.

{% hint style="info" %}
This test case does not use familial names to mimic contexts where only given names \(no surnames\) are present.
{% endhint %}

```javascript
{
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
            "value": "FHR-4956"
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
      }
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP code of 201 Created |
| SHOULD | PMIR Only | Include an OperationOutcome entry in the response |
| SHOULD |  | Include a Patient entry in response containing created patient |
| SHOULD |  | Include the RelatedPerson entry which was created |
| SHOULD |  | Include a link to the master identity with code refer  |

## Validate Child Patient Created

The test harness executes a query against the receiver to ensure the record was created domain

```http
GET http://sut:8080/fhir/Patient?identifier=http://ohie.org/test/test|FHR-4956 HTTP/1.1
Accept: application/fhir+json
Authorization: bearer XXXXXXX
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Accept the message with HTTP 200 OK |
| MUST |  | Include a bundle with exactly 1 patient result |
| MUST |  | Include a bundle with exactly 1 RelatedPerson result |
| MUST |  | Contain a patient for WIN MINH |
| MUST |  | Have an identifier for FHR-4956 in system http://ohie.org/test/test |
| MUST |  | Contain a RelatedPerson with name SU MYAT LWIN |
| SHOULD |  | Contain one or more link entries with type seealso pointing to local records |

## Register Mother Patient and Newborn Demographics in Transaction Bundle

The test harness sends an authenticated request to create a newborn record with the mother's demographics. This test mimics registering a patient \(the Mother\) and a nameless newborn \(the Baby\) in one transaction. 

Patient \(Mother\) details:

* Identifier `FHR-4837` in `http://ohie.org/test/test` with use `official`
* Name: SARAH ABELS
* Gender: Female
* DOB: 1984-05-25

Newborn information:

* Identifier `FHR-4837` in `http://ohie.org/test/test`
* Gender: Female
* DOB: 2021-04-25

{% hint style="info" %}
The bundle portrayed is using type `history` and is intended to be tested as part of a PMIR payload. You can also use the bundle as a simple POST of a transaction. 
{% endhint %}

```javascript
{
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
            "value": "FHR-4837"
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
        "id": "ohie-cr-05-20-fhir-mother-rp",
        "identifier": [
          {
            "use": "official",
            "system": "http://ohie.org/test/test",
            "value": "FHR-0844"
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
        ],
        "name": [
          {
            "use": "usual",
            "family": "Abels",
            "given": [
              "Sarah"
            ]
          }
        ],
        "gender": "female"
      }
    },
    {
      "fullUrl": "Patient/ohie-cr-05-20-fhir-mother",
      "resource": {
        "resourceType": "Patient",
        "id": "ohie-cr-05-20-fhir-mother",
        "identifier": [
          {
            "use": "normal",
            "system": "http://ohie.org/test/test",
            "value": "FHR-0844"
          }
        ],
        "name": [
          {
            "use": "usual",
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
            "other": "RelatedPerson/ohie-cr-05-20-fhir-mother-rp",
            "type": "see-also"
          }
        ]
      }
    }
  ]
}
```

### Expected Behaviour

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
      <td style="text-align:left">Return HTTP code of 201 Created</td>
    </tr>
    <tr>
      <td style="text-align:left">SHOULD</td>
      <td style="text-align:left">PMIR Only</td>
      <td style="text-align:left">Include an OperationOutcome entry in the response</td>
    </tr>
    <tr>
      <td style="text-align:left">SHOULD</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Include a Patient entry in response containing created patients for</p>
        <p>the newborn and mother.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SHOULD</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Include a link to the master identity with code refer</td>
    </tr>
  </tbody>
</table>

## Validate Newborn Patient Created

The test harness executes a query against the receiver to ensure the record was created domain

```http
GET http://sut:8080/fhir/Patient?identifier=http://ohie.org/test/test_a|FHR-4837&_include=RelatedPerson%3Apatient HTTP/1.1
Accept: application/fhir+json
Authorization: bearer XXXXXXX
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Accept the message with HTTP 200 OK |
| MUST |  | Include a bundle with exactly 1 patient result. |
| MUST |  | Contain the nameless newborn patient details \(validated by Gender and DOB\) |
| MUST |  | Have an identifier for FHR-4837 in system http://ohie.org/test/test |
| MUST |  | Have a RelatedPerson with identifier FHR-0844 for SARAH ABELS |
| SHOULD |  | Contain one or more link entries with type seealso pointing to local records |

## Validate Mother Patient Created with Link



