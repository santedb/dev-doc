---
description: Patent Demographics Query – Query by name
---

# TEST: OHIE-CR-12-HL7v2

This test ensures that the recipient of the query can perform an exact match on a patient’s name as provided in an admit message. The test will additionally test partial matching using phonetics and patterns. The recipient must pass one of the phonetic or pattern matching cases.

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Jennifer Jones, id: RJ-439^^^TEST, gender: F, dob: 1984-01-25

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-12-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||

```

## Test Step 1:

Test harness sends a PDQ message containing a name which is known to the receiver:

```text
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

```text
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





