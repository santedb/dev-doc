---
description: Patient Identity Feed - Blocks Unknown Identity Domain / Authority
---

# TEST: OHIE-CR-03-FHIR

This test validates that the receiving system rejects messages which contain identifiers which belong to identity domains which are not configured on the receiver.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)

## Discussion

The SanteMPI solution must have an understanding about identity domains for which patients may be assigned identifiers. This is how the CR/SanteMPI ensures that data is semantically correct, that the sender has proper authority over the identity domain, and how the SanteMPI solution can validate identifiers prior to persisting and matching.

## Pre-Conditions / Setup

Use the Assigning Authority panel to ensure that no domains are registered in either:

* http://ohie.org/test/test\_block , or
* 1.3.6.1.4.1.52820.3.72.5.9.4

You can verify this by executing the following queries against the SanteMPI server:

```http
GET http://sut:8080/hdsi/AssigningAuthority?url=http%3A%2F%2Fohie.org%2Ftest%2Ftest_block HTTP/1.1
GET http://sut:8080/hdsi/AssigningAuthority?oid=1.3.6.1.4.1.52820.3.72.5.9.4 HTTP/1.1
```

## Register Unknown Identity Domain \(via URL\)

The test harness sends a registration request to the receiver with `http://ohie.org/test/test_block` domain.

```javascript
{
  "resourceType": "Patient",
  "id": "1",
  "active": true,
  "identifier": [
    {
      "use": "usual",
      "system": "http://ohie.org/test/test_block",
      "value": "030",
      "assigner": {
        "display": "Fake Domain"
      }
    }
  ],
  "name": [
    {
      "use": "official",
      "family": "NOBODY",
      "given": [
        "NOTHING"
      ]
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = fatal-error |
| MUST |  | Include an OperationOutcome entry in the response |
| MUST |  | Indicate that the identity domain http://ohie.org/test/test\_block is not a valid identity domain. |
| MUST |  | Carry an HTTP response code in 400 series |
| SHOULD |  | Carry an HTTP response code of 422. |

## Register Unknown Identity Domain \(via OID\)

The test harness sends a registration request to the receiver with `urn:oid:1.3.6.1.4.1.52820.3.72.5.9.4` domain.

```javascript
{
  "resourceType": "Patient",
  "id": "1",
  "active": true,
  "identifier": [
    {
      "use": "usual",
      "system": "urn:oid:1.3.6.1.4.1.52820.3.72.5.9.4",
      "value": "031",
      "assigner": {
        "display": "Fake Domain"
      }
    }
  ],
  "name": [
    {
      "use": "official",
      "family": "NOBODY",
      "given": [
        "NOTHING"
      ]
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = fatal-error |
| MUST |  | Include an OperationOutcome entry in the response |
| MUST |  | Indicate that the identity domain urn:oid:1.3.6.1.4.1.52820.3.72.5.9.4 is not a valid identity domain. |
| MUST |  | Carry an HTTP response code in 400 series |
| SHOULD |  | Carry an HTTP response code of 422. |

