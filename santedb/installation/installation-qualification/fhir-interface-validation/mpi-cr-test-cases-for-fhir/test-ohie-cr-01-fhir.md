---
description: Mobile Patient Identity Feed - Invalid Registration Message
---

# TEST: OHIE-CR-01-FHIR

This test validates that the MPI/Client Registry rejects a poorly formed message.

## Discussion

The SanteMPI product solution, when configured properly, will perform basic validation in order to ensure that it can appropriately route and process FHIR registration messages to/from source systems. Because FHIR has very minimal requirements for patient information, this test merely ensures that minimal useful data is required including:

* Appropriate codification of objects \(such as name, addresses, telecommunications addresses, etc.\)
* Appropriate information to classify identity domains and assigning authority

## Pre-Conditions / Setup

None

## Register Incomplete Message

The test harness sends a patient which ahs a mal-formed identifier entry which is missing the system.

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
| MUST | PMIR Only | Reject the message with response.code = fatal-error |
| MUST |  | Include an OperationOutcome entry in response |
| MUST |  | Indicate that the resource failed validation. |
| MUST |  | Carry an HTTP response code in the 400 series |
| SHOULD |  | Carry an HTTP response code of 422 |

