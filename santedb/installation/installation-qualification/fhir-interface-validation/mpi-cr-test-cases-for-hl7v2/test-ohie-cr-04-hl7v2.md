---
description: Patient Identity Feed – Blocks invalid assigning authority
---

# TEST: OHIE-CR-04-HL7v2

This test ensures that two assigning authorities cannot assign identifiers from the other’s assigning domain. In this test, the harness mimics two authorities \(TEST\_HARNESS\_A and TEST\_HARNESS\_B\). They each register a patient and the harness then verifies that TEST\_HARNESS\_B does not assign an identifier from TEST\_HARNESS\_A’s identity domain.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.2 has assigning authority of TEST\_A which can be assigned from TEST\_HARNESS\_A

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.3 has assigning authority of TEST\_B which can be assigned from TEST\_HARNESS\_B

## Test Step 1:

Test harness \(as TEST\_HARNESS\_A\) sends ADT^A01 registering a new patient with an identifier from TEST\_A domain.

```text
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-04-20|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST_A||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I

```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_A\|TEST”
* Response is ACK^A01
* Response version is 2.3.1

## Test Step 2:

Test harness \(as TEST\_HARNESS\_B\) attempts to send an ADT^A01 for authority A.

```text
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-04-30|P|2.3.1
EVN||20101020
PID|||NFD-3049542-23^^^TEST_A||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Expected Behaviour

* Receiver rejects the message with an AE or AR
* An MSA message exists with an appropriate error code
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_B\|TEST”
* Response is ACK^A01
* Response Version is 2.3.1

