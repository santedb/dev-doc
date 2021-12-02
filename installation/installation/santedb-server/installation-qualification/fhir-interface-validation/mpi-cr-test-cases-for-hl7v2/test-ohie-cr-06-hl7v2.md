---
description: Patient Identity Feed – Update based on matching NID
---

# TEST: OHIE-CR-06-HL7v2

This test ensures that the receiver is able to merge patient data from an assigning authority (TEST\_A) which has an national patient identifier (assigning authority NID). The demographics data does not match, this is to test that matching is done on explicit identifiers.

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.2 has assigning authority of TEST\_A which can be assigned from TEST\_HARNESS\_A

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID which can be assigned from NID\_AUTH

#### Ensure that the following patient is registered in the receiver (can be done with the ADT message provided). Name: John Smith, id: NID-000345435^^^NID^NNXXX, gender: M, dob: 1980

```
MSH|^~\&|NID_AUTH^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-06-20|P|2.3.1
EVN||20101020
PID|||NID-000345435^^^NID^NNXXX||SMITH^JOHN^^^^^L||1980|M|||||||||||
PV1||I
```

## Test Step 1:

Test harness (as TEST\_HARNESS\_A) sends a registration message for patient Jon \[sic] Smith having a more specific date of birth, with NID of NID-000345435 and local identifier of TEST\_A of RJ-449.

```
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-06-30|P|2.3.1
EVN||20141001
PID|||RJ-449^^^TEST_A^PI~NID-000345435^^^NID^PI||SMITH^JON^^^^^L||198005|M|||||||||||||
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS|TEST”

## Test Step 2

Test harness verifies the record was linked with the NID by executing a PIX query

```
MSH|^~\&|TEST_HARNESS_A|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-06-40|P|2.5 
QPD|IHE PIX Query|Q0640|NID-000345435^^^NID^PI
RCP|I
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-449 in domain TEST\_A in one of the PID-3 repetitions
