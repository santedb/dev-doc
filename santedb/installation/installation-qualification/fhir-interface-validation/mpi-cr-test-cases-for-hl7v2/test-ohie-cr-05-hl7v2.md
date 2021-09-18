---
description: Patient Identity Feed – Minimal data set
---

# TEST: OHIE-CR-05-HL7v2

This test ensures that the receiver does not reject a message containing only an identifier, and one of gender, date of birth, mother’s identifier. This test makes no assertion about merging/matching patients

## Discussion

This test mimics the environment whereby a newborn demographic with minimal patient information \(gender and date of birth\) can be stored by the client registry and faithfully returned with an appropriate query to the interface.

## Pre-Conditions / Setup

All conditions from OHIE-CR-02 should be completed prior to running this test suite.

## Register Patient with Minimal Demographics

Test harness sends an ADT^A01 message with minimal data set containing information for a newborn with only an identifier, gender and date of birth.

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-05-20|P|2.3.1
EVN||20141001
PID|||RJ-441^^^TEST||||20141001|M||||||||||||| 
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an `AA`
* MSH-5 and MSH-6 matches `TEST_HARNESS|TEST`
* Response is `ACK^A01`
* Response is version `2.3.1`

## Query for Minimal Patient using Identifier

Test harness verifies the infant record was created in the receiver.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-05-30|P|2.5
QPD|IHE PIX Query|Q0530|RJ-441^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver responds with an `AA`
* Receiver sends exactly one `PID` segment with identifier `RJ-441` in domain `TEST` in PID-3



