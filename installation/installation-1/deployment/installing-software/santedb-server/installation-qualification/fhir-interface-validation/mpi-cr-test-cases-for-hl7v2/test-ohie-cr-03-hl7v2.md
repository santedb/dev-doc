---
description: Patient Identity Feed – Blocks unknown assigning authority
---

# TEST: OHIE-CR-03-HL7v2

This test ensures that the receiver rejects messages which contain identifiers assigned from authorities which are unknown.

## Discussion

It is expected that a patient identity cross reference manager will ensure that data is valid prior to recording patient registrations and performing cross reference functions.&#x20;

The lack of configuration for an identity domain being received by an identity source indicates a misconfiguration of the MPI and/or the identity source. This test ensures that configuration is consistent within a jurisdiction.

## Pre-Conditions / Setup

In order to mimic a mis-configuration of the client registry, the environment should ensure that the domain `TEST_BLOCK` and OID `2.16.840.1.113883.3.72.5.9.4` are not present.

{% hint style="info" %}
If the SanteMPI instance is configured to use Msh8 security and not node authentication, then the `MSH-8` value of all test messages must contain `TEST_HARNESS+TEST_HARNESS`
{% endhint %}

## Attempt Registration with invalid OID

Test harness sends ADT^A01 message having the invalid OID in CX.4.2.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20141104174451||ADT^A01^ADT_A01|TEST-CR-03-10|P|2.3.1
EVN||20101020
PID|||RJ-999-2^^^&2.16.840.1.113883.3.72.5.9.4&ISO||THAMES^ROBERT^^^^^L| |1983|M|||1220 Centennial Farm Road^^ELLIOTT^IA^51532||^PRN^PH^^^712^7670867||||||481-27-4185
PV1||I
```

### Expected Behaviour

* Receiver rejects message with error code AE or AR
* MSH-5 and MSH-6 matches “TEST\_HARNESS|TEST”
* Meaning MSA or ERR segment is conveyed showing the error
* Response is ACK^A01
* Response Version is 2.3.1

## Attempt Registration with invalid NamespaceID

Test harness sends ADT^A01 message having invalid assigning authority name in CX.4.1

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-03-20|P|2.3.1
EVN||20101020
PID|||RJ-999-2^^^TEST_BLOCK||THAMES^ROBERT^^^^^L| |1983|M|||1220 Centennial Farm Road^^ELLIOTT^IA^51532||^PRN^PH^^^712^7670867||||||481-27-4185
PV1||I
```

### Expected Behaviour

* Receiver rejects message with error code AE or AR
* MSH-5 and MSH-6 matches “TEST\_HARNESS|TEST”
* Meaning MSA or ERR segment is conveyed showing the error
* Response is ACK^A01
* Response Version is 2.3.1
