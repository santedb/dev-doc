---
description: Patient Identity Feed – Auto-fill CX.4 data
---

# TEST: OHIE-CR-02-HL7v2

This test validates that the Client Registry is capable of populating the CX.4.1 from CX.4.2 and CX.4.3 or vice-versa given partial data in the CX.4 field.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST

## Test Step 1:

Test harness sends ADT^A01 message where the CX.4.1 of the PID is missing but the message contains CX.4.2 and CX.4.3

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-02-10|P|2.3.1
EVN||20101020
PID|||RJ-438^^^&2.16.840.1.113883.3.72.5.9.1&ISO||JOHNSTON^ROBERT^^^^^L|MURRAY^^^^^^L|19830205|M|||1220 Centennial Farm Road^^ELLIOTT^IA^51532||^PRN^PH^^^712^7670867||||||481-27-4185
PV1||I

```

### Expected Behaviour

* Receiver Accepts Message with an AA
* Response is ACK^A01
* Response is version 2.3.1
* MSH-5 and MSH-6 matches “TEST\_HARNESS\|TEST”

## Test Step 2:

Test harness ensures that patient was registered and receiver has populated CX.4.1 from the CX.4.2 and CX.4.3 values by executing:

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-02-20|P|2.5
QPD|IHE PIX Query|Q0220|RJ-438^^^&2.16.840.1.113883.3.72.5.9.1&ISO^PI
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an AA
* Response is RSP^K23
* Response message contains exactly one PID segment
* PID-3 of PID segment contains an identifier having:
  * PID.3.4.1 = TEST
  * PID.3.4.2 = 2.16.840.1.113883.3.72.5.9.1
  * PID.3.4.3 = ISO

## Test Step 3:

Test harness sends ADT^A01 message where the CX.4.2 and CX.4.3 of the PID are missing but the message contains CX.4.1

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-02-30|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I

```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS\|TEST”

## Test Step 4:

Test harness ensures patient was registered and receiver has populated CX.4.2 and CX.4.3 from the CX.4.1 value provided by executing:

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-02-40|P|2.5
QPD|IHE PIX Query|Q0220|RJ-439^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an AA
* Response message contains exactly one PID segment
* PID-3 of PID segment contains an identifier having:
  * PID.3.4.1 = TEST
  * PID.3.4.2 = 2.16.840.1.113883.3.72.5.9.1
  * PID.3.4.3 = ISO

