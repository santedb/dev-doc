---
description: Valid Patient Identity Merge
---

# TEST: OHIE-CR-16-HL7v2

This test will ensure that the client registry can appropriately handle a merge condition whereby a local assigning authority notifies the client registry of a local merge \(two local identifiers are in fact the same person\).

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST which can be assigned from TEST\_HARNESS

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-16-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Jenn Jones, id: RJ-999^^^TEST, gender: F, dob: 1984-01

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-16-15|P|2.3.1
EVN||20101020
PID|||RJ-999^^^TEST||JONES^JENN^^^^^L||198401|F|||||||||||
PV1||I
```

## Test Step 1:

Test harness sends a query to verify there are two Jennifer Jones with identifiers assigned in TEST domain.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-16-20|P|2.5
QPD|Q22^Find Candidates^HL7|Q1620|@PID.5.1^JONES|||||^^^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends two PID segments one having identifier RJ-439 in domain TEST in PID-3 and another having RJ-999 in domain TEST in PID-3

## Test Step 2:

Test harness sends a merge message and instructs the recipient to merge identifier RJ-999 into record RJ-439.

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A40^ADT_A40|TEST-CR-16-30|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENN^^^^^L||198401|F|||||||||||
MRG|RJ-999^^^TEST
```

### Expected Behaviour

* Receiver responds with an AA

## Test Step 3:

Test harness verifies the identifier was merged using the following PIX query.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-16-40|P|2.5
QPD|IHE PIX Query|Q1640|RJ-439^^^TEST^PI|^^^TEST
RCP|I
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates data found by sending QAK of OK
* Receiver responds with exactly one PID segment having :
  * One PID-3 containing the RJ-439 identifier in domain TEST
  * One PID-3 containing the RJ-999 identifier in domain TEST

## Test Step 4:

Test harness verifies old identifier is de-referenced from patient record

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-16-50|P|2.5
QPD|IHE PIX Query|Q1650|RJ-999^^^TEST^PI|^^^TEST
RCP|I
```

### Expected Behaviour

* Receiver accepts the message with AE
* Receiver conveys no data found with AE in QAK
* Receiver indicates error by sending an ERR segment with QPD^1^3^1^1

## Test Step 5:

Test harness may send a query to verify there are still two Jennifer Jones in the target \(i.e. the old record still exists, but the identifiers were merely merged\).

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-16-60|P|2.5
QPD|Q22^Find Candidates^HL7|Q1660|@PID.5.1^JONES
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends two PID segments one having identifier RJ-439 and RJ-999 in domain TEST in PID-3 and another having no identifiers in domain TEST in PID-3

