---
description: Patient Identity Feed – Match with mother’s identifier
---

# TEST: OHIE-CR-07-HL7v2

This test ensures that the receiver is able to match an incoming patient with their mother via the “Mother’s Identifier” property. In this test, the harness with register a patient \(the mother\) and subsequently will register an infant record \(only dob, gender and id\) with the mother’s identifier attached. The test will ensure that the link occurred by validating a demographic query contains the mother’s name.

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST which can be assigned from TEST\_HARNESS

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-07-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Test Step 1:

Test harness sends an ADT^A01 message with minimal data set containing information for a newborn with only an identifier, gender and date of birth with mother’s identifier.

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-07-20|P|2.3.1
EVN||20101020
PID|||RJ-440^^^TEST||||20141001|M|||||||||||||RJ-439^^^TEST
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS\|TEST”

## Test Step 2:

Test harness verifies the infant record was created in the receiver.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-07-30|P|2.5 
QPD|IHE PIX Query|Q0530|RJ-440^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-440 in domain TEST in PID-3

## Test Step 3:

Test harness verifies the infant record has mother’s information attached to it by sending a PDQ message with infant’s identifier.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-07-40|P|2.5
QPD|Q22^Find Candidates^HL7|Q0740|@PID.3.1^RJ-440~@PID.3.4.1^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-440 in domain TEST in PID-3
* Receiver conveys mother’s name in PID-6 with value of JONES^JENNIFER
* Receiver conveys mother’s identifier in PID-21 of RJ-439 in domain TEST





