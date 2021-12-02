---
description: >-
  Patient Identity Query – Identifier query with specific request response
  domains
---

# TEST: OHIE-CR-10-HL7v2

In this test, the test harness will register a patient with a local identifier \(TEST domain\). The receiver is the assigning authority for the ECID domain and should generate an ECID by whatever means the software performs this task. The test harness will then ask the receiver to do a cross reference between the TEST domain and the ECID domain. This test ensures that the receiver adheres to the “What Domains Returned” query parameter.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID

#### Ensure a patient with the following information is registered in the receiver:Name: Betty Boop, ID: RJ-444 in domain TEST, DOB: 1935This can be registered by sending the following message to the recipient:

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-09-30|P|2.3.1
EVN||20101020
PID|||RJ-444^^^TEST||BOOP^BETTY^^^^^L||1935|F|||
PV1||I
```

## Test Step 1:

Test harness requests the receiver to explicitly give it the TEST domain identifiers by sending:

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-10-20|P|2.5 
QPD|IHE PIX Query|Q1020|RJ-444^^^TEST^PI|^^^TEST
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an AA
* QAK of OK
* Response message contains exactly one PID segment
* PID contains exactly one PID-3 having:
  * PID.3.1.1 = RJ-444
  * PID.3.4.1 = TEST
  * PID.3.4.2 = 2.16.840.1.113883.3.72.5.9.1

## Test Step 2:

Test harness requests the receiver to explicitly give it the domain identifiers from an invalid domain \(RANDOM\) by sending:

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-10-30|P|2.5
QPD|IHE PIX Query|Q1030|RJ-444^^^TEST^PI|^^^RANDOM
RCP|I
```

### Expected Behaviour

* Receiver rejects the message with an AE
* Receiver indicates query error with QAK of AE
* Receiver indicates the error with ERR having QPD^1^4

## Test Step 3:

Test harness requests the receiver to explicitly give it the domain identifier from a valid domain \(NID\) for which no identifiers have been associated with the patient by sending:

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-10-40|P|2.5
QPD|IHE PIX Query|Q1040|RJ-444^^^TEST^PI|^^^NID
RCP|I
```

### Expected Behaviour:

* Receiver accepts the message with AA
* Receiver indicates no data found with QAK of NF
* No PID segments are sent in the response message.



