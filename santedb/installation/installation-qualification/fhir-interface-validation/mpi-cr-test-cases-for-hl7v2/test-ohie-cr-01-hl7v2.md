---
description: Patient Identity Feed – Invalid register patient message
---

# TEST: OHIE-CR-01-HL7v2

This test validates that the Client Registry rejects a poorly formed message lacking appropriate assigner information in PID-3

## References

## Pre-Conditions / Setup



## Test Step 1:

Test harness sends ADT^A01 message where the CX.4 of the PID is missing.

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01| TEST-CR-01-10|P|2.3.1
EVN||20101020
PID|||RJ-438^^^&&||JOHNSTON^ROBERT^^^^^L|MURRAY^^^^^^L|19830205|M|||1220 Centennial Farm Road^^ELLIOTT^IA^51532||^PRN^PH^^^712^7670867||||||481-27-4185
PV1||I

```

### Expected Behaviour

* Receiver rejects the message with an AR or AE
* Response is ACK^A01
* Response version is 2.3.1



