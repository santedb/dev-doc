---
description: >-
  Patient Identity Feed – Auto-merge between patients with matching NID (as non
  medical ID)
---

# TEST: OHIE-CR-18-HL7v2

This test ensures that the receiver is able to merge patient data from an assigning authority (TEST\_A) which has an national identifier (not assigned by central authority as a PID). The demographics data does not match, this is to test that matching is done on explicit identifiers.

Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.2 has assigning authority of TEST\_A which can be assigned from TEST\_HARNESS\_A

Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.B has assigning authority of TEST\_A which can be assigned from TEST\_HARNESS\_B

Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.9 has assigning authority of NID

Perform necessary steps to ensure that the receiver is configured to merge patients based on the SSN field (PID-19)

## Test Step 1:

Test harness (as TEST\_HARNESS\_A) sends a registration message for patient Yannick Jones having a date of birth to the month, with NID of NID-000345439 and local identifier of TEST\_A of RJ-460.

```
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-18-20|P|2.3.1
EVN||20141001
PID|||RJ-460^^^TEST_A||JONES^YANNICK^^^^^L||199004|M|||||||||||NID-000345439^^^NID
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_A|TEST”

## Test Step 2:

Test harness (as TEST\_HARNESS\_B) sends a registration message for patient Yan Jones having a more specific date of birth, with NID of NID-000345439 and local identifier of TEST\_B of RB-469.

```
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-18-30|P|2.3.1
EVN||20141001
PID|||RB-469^^^TEST_B||JONES^YAN^^^^^L||19900404|M|||||||||||NID-000345439^^^NID
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_B|TEST”

## Test Step 3:

Test harness verifies the record from TEST\_B is linked with TEST\_A via the NID

```
MSH|^~\&|TEST_HARNESS_A|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-06-40|P|2.5
QPD|IHE PIX Query|RB-469^^^NID^PI
RCP|I
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-449 in domain TEST\_A in one of the PID-3 repetitions
