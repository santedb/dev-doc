---
description: Mobile Patient Identity Feed - Invalid Registration Message
---

# TEST: OHIE-CR-01-FHIR

This test validates that the MPI/Client Registry rejects a poorly formed message.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)

## Discussion

The SanteMPI product solution, when configured properly, will perform basic validation in order to ensure that it can appropriately route and process FHIR registration messages to/from source systems. Because FHIR has very minimal requirements for patient information, this test merely ensures that minimal useful data is required including:

* Appropriate codification of objects \(such as name, addresses, telecommunications addresses, etc.\)
* Appropriate information to classify identity domains and assigning authority

## Pre-Conditions / Setup

None

## Register Incomplete Message

The test harness sends a patient which has a malformed identifier entry which is missing the system.

```javascript
{
  "resourceType": "Patient",
  "id": "1",
  "active": true,
  "identifier": [
    {
      "use": "usual",
      "value": "12345",
      "assigner": {
        "display": "Fake Domain"
      }
    }
  ],
  "name": [
    {
      "use": "official",
      "family": "JOHNSTON",
      "given": [
        "ROBERT"
      ]
    }
  ],
  "telecom": [
    {
      "use": "home"
    },
    {
      "system": "phone",
      "value": "(712) 767-0867",
      "use": "home",
      "rank": 1
    }
  ],
  "gender": "male",
  "birthDate": "1983-02-05",
  "deceasedBoolean": false,
  "address": [
    {
      "use": "home",
      "type": "both",
      "line": [
        "1220 Centennial Farm Road"
      ],
      "city": "ELLIOTT",
      "state": "IA",
      "postalCode": "51532"
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = fatal-error |
| MUST |  | Include an OperationOutcome entry in response |
| MUST |  | Indicate that the resource failed validation. |
| MUST |  | Carry an HTTP response code in the 400 series |
| SHOULD |  | Carry an HTTP response code of 422 |

## Invalid / Unknown Reference

This test will ensure that the client registry rejects a message \(such as a transaction or PMIR bundle\) where a target of a relationship is unknown. 

{% hint style="info" %}
This test attempts to establish whether the Client Registry is capable of maintaining referential integrity between resources. This is important as, when configuring matching, data which is linked must be available to the matching engine at all times and missing or broken link data may result in partial / useless records.
{% endhint %}

```javascript
{
  "resourceType": "Patient",
  "id": "1",
  "active": true,
  "name": [
    {
      "use": "official",
      "family": "JOHNSTON",
      "given": [
        "ROBERT"
      ]
    }
  ],
  "telecom": [
    {
      "use": "home"
    },
    {
      "system": "phone",
      "value": "(712) 767-0867",
      "use": "home",
      "rank": 1
    }
  ],
  "gender": "male",
  "birthDate": "1983-02-05",
  "deceasedBoolean": false,
  "address": [
    {
      "use": "home",
      "type": "both",
      "line": [
        "1220 Centennial Farm Road"
      ],
      "city": "ELLIOTT",
      "state": "IA",
      "postalCode": "51532"
    }
  ],
  "managingOrganization" : {
    "reference" : "Organization/3930293029302923"
  }
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
      <td style="text-align:left">Return MessageHeader with response.code = fatal-error</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Include an OperationOutcome entry in response</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Indicate that the resource failed validation and/or that the reason for</p>
        <p>rejection was an unresolvable reference.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Carry an HTTP response code in the 400 series</td>
    </tr>
    <tr>
      <td style="text-align:left">SHOULD</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Carry an HTTP response code of 422 or 404</td>
    </tr>
  </tbody>
</table>

## 

