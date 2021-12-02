---
description: Patient Demographics Query – Identifier query
---

# TEST: OHIE-CR-11-HL7v2

This test case ensures that the recipient of the query can perform a patient demographics query based on the PID-3 values provided in an admit message.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID

#### Ensure that the following patient is registered in the receiver (can be done with the ADT message provided). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-11-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

## Test Step 1:

Test harness sends a PDQ message containing a patient identifier which is known to the receiver:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-11-20|P|2.5
QPD|Q22^Find Candidates^HL7|Q1120|@PID.3.1^RJ-439~@PID.3.4.1^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* QAK segment contains OK
* Response contains a PID segment containing:
  * PID-3=439^^^TEST
  * PID-5=JONES^JENNIFER
  * PID-6=19840125

## Test Step 2:

Test harness sends a PDQ message containing a patient identifier which is unknown to the receiver:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-11-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q1130|@PID.3.1^RJ-9483~@PID.3.4.1^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts the message with AA
* QAK segment contains NF
* Response contains no PID segments

## Test Step 3:

Test harness sends a PDQ message with an invalid query parameter of @PID.3.4.99

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-11-40|P|2.5
QPD|Q22^Find Candidates^HL7|Q1140|@PID.3.1^RJ-9483~@PID.3.4.99^NOVALUE
RCP|I|10^RD
```

### Expected Behaviour

* Receiver rejects the message with AR or AE
* QAK segment contains AE
* Response contains no PID segments

## Test Step 4:

Test harness sends a PDQ message and specifies what domains should be returned in the QPD-8 containing a valid domain of TEST

```
TESTMSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-11-50|P|2.5
QPD|Q22^Find Candidates^HL7|Q1150|@PID.3.1^RJ-439~@PID.3.4.1^TEST|||||^^^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts message with an AA
* QAK segment contains OK
* Response contains exactly one PID segment
  * PID-3 (Exactly one)=439^^^TEST
  * PID-5=JONES^JENNIFER
  * PID-6=19840125

## Test Step 5:

Test harness sends a PDQ message and specifies what domains should be returned in QPD-8 with a valid domain of NID which has no matching identifiers.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-11-60|P|2.5
QPD|Q22^Find Candidates^HL7|Q1160|@PID.3.1^RJ-439~@PID.3.4.1^TEST|||||^^^NID
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts message with an AA
* QAK segment contains NF
* No PID segments are returned in the response

## Test Step 6:

Test harness sends a PDQ message and specifies what domains should be returned in QPD-8 with an invalid domain of RANDOM.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-11-70|P|2.5
QPD|Q22^Find Candidates^HL7|Q1170|@PID.3.1^RJ-439~@PID.3.4.1^TEST|||||^^^RANDOM
RCP|I|10^RD
```

### Expected Behaviour

* Receiver rejects the message with AE
* Receiver indicates query error with QAK of AE
* No PID segments are returned
* Receiver indicates QPD^1^8 in the ERR segment
