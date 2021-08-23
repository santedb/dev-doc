---
description: Patient Identity Merge No Assigning Authority
---

# TEST: OHIE-CR-17-HL7v2

This test will ensure that the client registry appropriately handles a merge condition whereby the local authority has not assigning authority to perform or merge the identifiers provided. This test will also ensure that merges across assigning authorities cannot be performed

## References

## Pre-Conditions / Setup

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.2 has assigning authority of TEST\_A which can be assigned from TEST\_HARNESS\_A

#### Setup the receiver so that OID 2.16.840.1.113883.3.72.5.9.3 has assigning authority of TEST\_B which can be assigned from TEST\_HARNESS\_B

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Sam Smith, id: RJ-203^^^TEST\_A, gender: F, dob: 1989-02-25

```text
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-17-15|P|2.3.1
EVN||20101020
PID|||RJ-203^^^TEST_A||SMITH^SAM^^^^^L||19890225|F|||||||||||
PV1||I
```

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Samantha Smith, id: RJ-292^^^TEST\_A, gender: F, dob: 1989-02

```text
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-17-20|P|2.3.1
EVN||20101020
PID|||RJ-292^^^TEST_A||SMITH^SAMANTHA^^^^^L||198902|F|||||||||||
PV1||I
```

#### Ensure that the following patient is registered in the receiver \(can be done with the ADT message provided\). Name: Samantha Smith, id: SJ-204^^^TEST\_B, gender: F, dob: 1989-02

```text
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-17-25|P|2.3.1
EVN||20101020
PID|||SJ-204^^^TEST_B||SMITH^SAMANTHA^^^^^L||198902|F|||||||||||
PV1||I
```

## Test Step 1:

Test harness \(as TEST\_HARNESS\_B\) sends ADT^A40 message attempting to merge identities from TEST\_A domain.

```text
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A40^ADT_A40|TEST-CR-17-30|P|2.3.1
EVN||20101020
PID|||RJ-203^^^TEST_A||SMITH^SAM^^^^^L||198902|F|||||||||||
MRG|RJ-292^^^TEST_A
```

### Expected Behaviour

* Receiver rejects message with an AE
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_B\|TEST”
* An ERR segment exists identifying the error

## Test Step 2:

Test harness \(as TEST\_HARNESS\_B\) sends ADT^A40 message attempting to merge across domains by instructing the receiver to merge an identifier from TEST\_A into TEST\_B.

```text
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A40^ADT_A40|TEST-CR-17-40|P|2.3.1
EVN||20101020
PID|||SJ-204^^^TEST_B||SMITH^SAM^^^^^L||198902|F|||||||||||
MRG|RJ-292^^^TEST_A
```

### Expected Behaviour

* Receiver rejects message with an AE or AR
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_B\|TEST”
* An ERR segment exists identifying the error

## Test Step 3:

Test harness \(as TEST\_HARNESS\_B\) sends ADT^A40 message attempting to merge a patient identifier which does not exist.

```text
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A40^ADT_A40|TEST-CR-17-50|P|2.3.1
EVN||20101020
PID|||SJ-204^^^TEST_B||SMITH^SAM^^^^^L||198902|F|||||||||||
MRG|RJ-292^^^TEST_B
```

### Expected Behaviour

* Receiver rejects message with an AE or AR
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_B\|TEST”
* An ERR segment exists identifying the error with HL7 code of 204 \(key does not exist\)

