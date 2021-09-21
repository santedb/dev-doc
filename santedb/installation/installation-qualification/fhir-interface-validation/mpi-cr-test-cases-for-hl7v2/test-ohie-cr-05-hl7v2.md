---
description: Patient Identity Feed – Minimal data set
---

# TEST: OHIE-CR-05-HL7v2

This test ensures that the receiver does not reject a message containing only an identifier, and one of gender, date of birth, mother’s identifier. This test makes no assertion about merging/matching patients

## Discussion

This test mimics the environment whereby a newborn demographic with minimal patient information \(gender and date of birth\) can be stored by the client registry and faithfully returned with an appropriate query to the interface.

This test validates the MPI/CR's ability to link a mother's record with a newborn's record, and to query that data back from the MPI. This option uses the Pediatrics Demographics Option in section `8.2.1` of the [IHE Patient Demographics Query](https://profiles.ihe.net/ITI/TF/Volume1/ch-8.html) 

{% hint style="info" %}
This test is only required if the Client Registry is implementing the Pediatrics option and supports the ability to query/link mothers with children.
{% endhint %}

## Pre-Conditions / Setup

All conditions from OHIE-CR-02 should be completed prior to running this test suite.

## Register Mother's Demographic

The test harness sends an ADT^A01 message with the mother's patient demographics

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-05-10|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^M|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

## Register Patient with Minimal Demographics

Test harness sends an ADT^A01 message with minimal data set containing information for a newborn with only an identifier, gender and date of birth. The PID-6 \(Mother's Maiden Name\), PID-21 \(Mother's Identifier\), and PID-24 \(Multiple Birth Indicator\).

```text
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-05-20|P|2.3.1
EVN||20141001
PID|||RJ-441^^^TEST|||JONES^JENNIFER|20141001|M|||||||||||||RJ-439^^^TEST|||1 
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an `AA`
* MSH-5 and MSH-6 matches `TEST_HARNESS|TEST`
* Response is `ACK^A01`
* Response is version `2.3.1`

## Query for Minimal Patient using Patient's Identifier

Test harness verifies the infant record was created in the receiver.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-05-30|P|2.5
QPD|IHE PIX Query|Q0530|RJ-441^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver responds with an `AA`
* Receiver sends exactly one `PID` segment with identifier `RJ-441` in domain `TEST` in PID-3

## Query for Newborn using Mother's Identifier

Test harness verifies the receiver can resolve the newborn demographic based on the identifier of the mother.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q22^QBP_Q22|TEST-CR-05-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q0540|@PID.21.1^RJ-439~@PID.21.3.4^TEST
RCP|I
```

### Expected Behaviour

* Receiver responds with an `AA`
* Receiver sends exactly one `PID` segment with identifier `RJ-441` in domain `TEST` in PID-3

