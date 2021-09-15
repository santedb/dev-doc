---
description: Patient Identity Feed – Blocks invalid assigning authority
---

# TEST: OHIE-CR-04-HL7v2

This test ensures that two sources cannot assign identifiers from the other’s assigning domain. In this test, the harness mimics two authorities \(TEST\_HARNESS\_A and TEST\_HARNESS\_B\). They each register a patient and the harness then verifies that TEST\_HARNESS\_B does not assign an identifier from TEST\_HARNESS\_A’s identity domain.

## Discussion

While not a hard requirement of the IHE Patient Identity Cross Referencing specification, it is important to ensure that identity sources are governed in a manner which ensures that cross-domain registrations/merges/modifications are performed. 

[IHE ITI-8 TF Vol 2a](https://profiles.ihe.net/ITI/TF/Volume2/ITI-8.html) indicates that the association of identity sources with their assigning authority be a supported feature, particularly in section 3.8.4.1.3.1:

> Patient Identity Source for the domain. This is expected to be the MSH-3 Sending Application and the corresponding MSH-4 Sending Facility fields in the HL7 ADT message. \(Alternative identification schemes might include IP address of the Patient Identity Source or Node Authentication if the Audit Trail and Node Authentication Integration Profile is used.\)

{% hint style="info" %}
This test represents a test of the ability of the client registry to perform basic governance of data submissions. This test case may not be a requirement in all jurisdictions. 
{% endhint %}

## Pre-Conditions / Setup

Prior to executing the tests in this test case, the system under test should be configured such that:

* Application `TEST_HARNESS_A` is configured
* Application `TEST_HARNESS_B` is configured
* Device `TEST_HARNESS_A|TEST` is configured 
* Device `TEST_HARNESS_B|TEST` is configured
* Authority `TEST_A` with OID `2.16.840.1.113883.3.72.5.9.2` is configured and `TEST_HARNESS_A` is granted authority to assign identifiers in this domain
* Authority `TEST_B` with OID `2.16.840.1.113883.3.72.5.9.3` is configured and `TEST_HARNESS_B` is granted authority to assign identifiers in this domain.



## Test Step 1:

Test harness \(as TEST\_HARNESS\_A\) sends ADT^A01 registering a new patient with an identifier from TEST\_A domain.

```text
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-04-20|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST_A||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_A\|TEST”
* Response is ACK^A01
* Response version is 2.3.1

## Test Step 2:

Test harness \(as TEST\_HARNESS\_B\) attempts to send an ADT^A01 for authority A.

```text
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-04-30|P|2.3.1
EVN||20101020
PID|||NFD-3049542-23^^^TEST_A||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Expected Behaviour

* Receiver rejects the message with an AE or AR
* An MSA message exists with an appropriate error code
* MSH-5 and MSH-6 matches “TEST\_HARNESS\_B\|TEST”
* Response is ACK^A01
* Response Version is 2.3.1

