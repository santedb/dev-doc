---
description: Patient Demographics Query – Query by date of birth
---

# TEST: OHIE-CR-14-HL7v2

This test ensures that the recipient supports the semantics of date matching and approximate matches by date range. This test case will query for an exact date of birth as provided in an admit message, and a fuzzy date of birth \(year, and year/month\).

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST which can be assigned from TEST\_HARNESS

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-14-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

## Test Step 1:

Test harness sends a query with date of birth precise to the year in which a patient’s date of birth falls.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-14-20|P|2.5
QPD|Q22^Find Candidates^HL7|Q1420|@PID.7^1984
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends exactly one PID segment with identifier RJ-439 in domain TEST in PID-3

## Test Step 2:

Test harness sends a query with date of birth precise to the month in which the patient’s date of birth falls.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-14-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q1430|@PID.7^198401
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends exactly one PID segment with identifier RJ-439 in domain TEST in PID-3

## Test Step 3:

Test harness sends a query with date of birth precise to the day in which a patient’s date of birth falls.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-14-40|P|2.5
QPD|Q22^Find Candidates^HL7|Q1440|@PID.7^19840125
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends exactly one PID segment with identifier RJ-439 in domain TEST in PID-3

## Test Step 4:

Test harness sends a query with date of birth precise to the year in which the patient’s date of birth does not fall.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-14-50|P|2.5
QPD|Q22^Find Candidates^HL7|Q1450|@PID.7^1900
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates no records found with QAK of NF
* Receiver sends no PID segments

