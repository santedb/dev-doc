---
description: Patient Identity Feed – Invalid register patient message
---

# TEST: OHIE-CR-01-HL7v2

This test validates that the Client Registry rejects a poorly formed message lacking appropriate assigner information in PID-3

## References

## Pre-Conditions / Setup



## Test Step 1:

Test harness sends ADT^A01 message where the CX.4 of the PID is missing.

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
|  |  | Receiver rejects the message with an AR or AE |
|  |  | Response is ACK^A01 |
|  |  | Response version is 2.3.1 |

## 



