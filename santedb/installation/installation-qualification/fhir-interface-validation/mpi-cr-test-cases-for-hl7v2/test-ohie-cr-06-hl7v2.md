---
description: Patient Identity Feed – Update based on matching NID
---

# TEST: OHIE-CR-06-HL7v2

This test ensures that the receiver is able to merge patient data from an assigning authority \(TEST\_A\) which has an national patient identifier \(assigning authority NID\). The demographics data does not match, this is to test that matching is done on explicit identifiers.

## References

## Pre-Conditions / Setup

## Test Step 1:

Test harness \(as TEST\_HARNESS\_A\) sends a registration message for patient Jon \[sic\] Smith having a more specific date of birth, with NID of NID-000345435 and local identifier of TEST\_A of RJ-449.

```text
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-06-30|P|2.3.1
EVN||20141001
PID|||RJ-449^^^TEST_A^PI~NID-000345435^^^NID^PI||SMITH^JON^^^^^L||198005|M|||||||||||||
PV1||I
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
|  |  | Receiver Accepts Message with an AA |
|  |  | MSH-5 and MSH-6 matches “TEST\_HARNESS\|TEST” |

## Test Step 2

Test harness verifies the record was linked with the NID by executing a PIX query

```text
MSH|^~\&|TEST_HARNESS_A|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-06-40|P|2.5 
QPD|IHE PIX Query|Q0640|NID-000345435^^^NID^PI
RCP|I
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
|  |  | Receiver responds with an AA |
|  |  | Receiver sends exactly one PID segment with identifier RJ-449 in domain TEST\_A in one of the PID-3 repetitions |

