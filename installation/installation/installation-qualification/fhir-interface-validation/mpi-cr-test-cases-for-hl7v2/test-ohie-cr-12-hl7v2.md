---
description: Patent Demographics Query – Query by name
---

# TEST: OHIE-CR-12-HL7v2

This test ensures that the recipient of the query can perform an exact match on a patient’s name as provided in an admit message. The test will additionally test partial matching using phonetics and patterns. The recipient must pass one of the phonetic or pattern matching cases.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID

#### Ensure that the following patient is registered in the receiver (can be done with the ADT message provided). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-12-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||

```

## Test Step 1:

Test harness sends a PDQ message containing a name which is known to the receiver:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-20|P|2.5
QPD|Q22^Find Candidates^HL7|Q1220|@PID.5.1^JONES~@PID.5.2^JENNIFER
RCP|I|10^RD
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* QAK segment contains OK
* Response contains a PID segment containing:
  * Response contains a PID segment containing:
  * PID-5=JONES^JENNIFER
  * PID-6=19840125

## Test Step 2:

Test harness sends a PDQ message containing a patient name which is unknown to the receiver:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q1230|@PID.5.1^HOOD~@PID.5.2^ROBIN
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts the message with AA
* QAK segment contains NF
* Response contains no PID segments

## Test Step 3:

Test harness sends a PDQ message containing a name which is known to the receiver, and indicates a domains to be returned of TEST in QPD-8.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-40|P|2.5
QPD|Q22^Find Candidates^HL7|Q1240|@PID.5.1^JONES~@PID.5.2^JENNIFER|||||^^^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* QAK segment contains OK
* Response contains exactly one PID segment containing:
  * PID-3 (Exactly one)=439^^^TEST
  * PID-5=JONES^JENNIFER
  * PID-6=19840125

## Test Step 4:

Test harness sends a PDQ message containing a patient name which is known to the receiver and indicates a domains to be returned which is invalid in QPD-8:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-45|P|2.5
QPD|Q22^Find Candidates^HL7|Q1245|@PID.5.1^JONES~@PID.5.2^JENNIFER|||||^^^RANDOM
RCP|I|10^RD
```

### Expected Behaviour:

* Receiver rejects the message with AE
* Receiver indicates query error with QAK of AE
* No PID segments are returned
* Receiver indicates QPD^1^8 in the ERR segment

## Test Step 5:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-50|P|2.5
QPD|Q22^Find Candidates^HL7|Q1250|@PID.5.1^JO*~@PID.5.2^JEN*|||||
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts the message with an AA
* Receiver indicates query success of OK in QAK
* Receiver returns at least one PID segment containing the match for Jennifer Jones
* Receiver sends a QRI segment with a QRI-3 indicating pattern match and strength of the match

## Test Step 6:

Test harness sends a PDQ message containing a phonetically equivalent name of a known patient to the receiver:Test harness sends a PDQ message containing a wildcard match which is known to the receiver:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-60|P|2.5
QPD|Q22^Find Candidates^HL7|Q1260|@PID.5.1^JONEZ~@PID.5.2^JENIPHER|||||
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts the message with an AA
* Receiver indicates query success of OK in QAK
* Receiver returns at least one PID segment containing the match for Jennifer Jones
* Receiver sends a QRI segment with a QRI-3 indicating phonetic match and strength of the match

## Test Step 7:

Test harness sends a PDQ message containing a name variant match which is known to the receiver:

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-12-70|P|2.5
QPD|Q22^Find Candidates^HL7|Q1270|@PID.5.1^JONES~@PID.5.2^JENN|||||
RCP|I|10^RD
```

### Expected Behaviour

* Receiver accepts the message with an AA
* Receiver indicates query success of OK in QAK
* Receiver returns at least one PID segment containing the match for Jennifer Jones
* Receiver sends a QRI segment with a QRI-3 indicating variant match and strength of the match
