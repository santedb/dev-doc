---
description: Patient Demographics Query – Query by multiple demographics fields
---

# TEST: OHIE-CR-15-HL7v2

This test ensures that the recipient of the query can perform a query on a series of demographics fields. The test harness will perform a query on a series of combinations of parameters such as name + gender, name + date of birth, gender + date of birth.

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST which can be assigned from TEST\_HARNESS

#### Ensure that the following patient is registered in the receiver (can be done with the ADT message provided). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```
Ensure that the following patient is registered in the receiver (can be done with the ADT message provided). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

## Test Step 1:

Test harness sends a query with patient’s name and gender which results in a match.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-15-20|P|2.5
QPD|Q22^Find Candidates^HL7|Q1520|@PID.8^F~@PID.5.1^JONES
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends exactly one PID segment with identifier RJ-439 in domain TEST in PID-3

## Test Step 2:

Test harness sends a query with fuzzy date of birth and patient’s name which results in a match.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-15-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q1530|@PID.7^1984~@PID.5.1^JONES~@PID.5.2^JENNIFER
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends exactly one PID segment with identifier RJ-439 in domain TEST in PID-3

## Test Step 3:

Test harness sends a query with date of birth precise to the day in which a gender which results in a match.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-15-40|P|2.5
QPD|Q22^Find Candidates^HL7|Q1540|@PID.7^19840125~@PID.8^F
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates records found with QAK of OK
* Receiver sends exactly one PID segment with identifier RJ-439 in domain TEST in PID-3

## Test Step 4:

Test harness sends a query with patient’s name and gender which results in no match.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-15-50|P|2.5
QPD|Q22^Find Candidates^HL7|Q1550|@PID.8^M~@PID.5.1^JONES~@PID.5.2^JENNIFER
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates no records found with QAK of NF
* Receiver sends no PID segments

## Test Step 5:

Test harness sends a query with fuzzy date of birth and patient’s name which results in no match.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-15-60|P|2.5
QPD|Q22^Find Candidates^HL7|Q1560|@PID.7^1984~@PID.5.1^JONES~@PID.5.2^JASON
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver indicates no records found with QAK of NF
* Receiver sends no PID segments

###
