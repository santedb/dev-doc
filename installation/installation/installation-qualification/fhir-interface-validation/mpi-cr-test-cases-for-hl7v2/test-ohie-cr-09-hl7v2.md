---
description: Patient Identity Query – Identifier query
---

# TEST: OHIE-CR-09-HL7v2

In this test, the test harness will register a patient with a local identifier (TEST domain) and will subsequently query the receiver to retrieve the identifiers linked to the newly registered patient.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID

## Test Step 1:

Test harness sends PIX query for identifier RJ-443 (an un-registered patient) and validates the receiver behaves appropriately.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-09-10|P|2.5 
QPD|IHE PIX Query|Q0910|RJ-443^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver accepts the message with AE
* Receiver conveys no data found with AE in QAK
* Receiver indicates error by sending an ERR segment with QPD^1^3^1^1

## Test Step 2:

Test harness sends PIX query for identifier RJ-443 (an un-registered patient) in domain RANDOM (an un-registered) domain

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-09-20|P|2.5
QPD|IHE PIX Query|Q0920|RJ-443^^^RANDOM^PI
RCP|I
```

### Expected Behaviour

* Receiver rejects the message with AE
* Receiver conveys query error with AE in QAK
* Receiver indicates error by sending an ERR segment with QPD^1^3^4^1

## Test Step 3:

Test harness sends ADT^A01 message registering a patient.

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-09-30|P|2.3.1
EVN||20101020
PID|||RJ-443^^^TEST||SMITH^STEPHANIE^^^^^L||198306|F|||
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS|TEST”

## Test Step 4:

Test harness ensures that patient was registered by executing:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-09-40|P|2.5
QPD|IHE PIX Query|Q0940|RJ-443^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an AA
* Response message contains exactly one PID segment
* QAK of OK
* PID-3 of PID segment contains an identifier having:
  * PID.3.1.1 = RJ-443
  * PID.3.4.1 = TEST
  * PID.3.4.2 = 2.16.840.1.113883.3.72.5.9.1
  * PID.3.4.3 = ISO
