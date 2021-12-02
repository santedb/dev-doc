---
description: Patient Demographics Query – Query by mother’s identifier
---

# TEST: OHIE-CR-13-HL7v2

This test ensures that the recipient of the query can perform a query by the patient’s mother’s identifier.

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST which can be assigned from TEST\_HARNESS

#### Ensure that the following patient is registered in the receiver (can be done with the ADT message provided). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-13-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

#### Ensure that the following patient is registered in the receiver (can be done with the ADT message provided).RJ-440^^^TEST, gender: M, DOB: 2014-10-01

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-13-15|P|2.3.1
EVN||20101020
PID|||RJ-440^^^TEST||||20141001|M|||||||||||||RJ-439^^^TEST
PV1||I
```

## Test Step 1:

Test harness sends a query with mother’s identifier components specified.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-13-20|P|2.5
QPD|Q22^Find Candidates^HL7|Q1320|@PID.21.1^RJ-439~@PID.21.4.1^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-440 in domain TEST in PID-3

## Test Step 2:

Test harness verifies the infant record was created in the receiver.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-13-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q0740|@PID.6.1^JONES~@PID.6.2^JENNIFER
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-440 in domain TEST in PID-3
