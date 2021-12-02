---
description: Patient Identity Feed – Invalid register patient message
---

# TEST: OHIE-CR-01-HL7v2

This test validates that the Client Registry rejects a poorly formed message lacking appropriate assigner information in PID-3.&#x20;

## Pre-Conditions / Setup

Prior to executing this test, SanteMPI instances should configure:&#x20;

* The `TEST_OTHER` application
* The `TEST_OTHER|TEST` device

{% tabs %}
{% tab title="Dataset" %}
```markup
<dataset id="Test Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <insert skipIfError="false" skipIfExists="true">
    <SecurityApplication xmlns="http://santedb.org/model">
      <id>F0FC4322-948D-4986-A06C-DA603A77EDDE</id>
      <!-- Secret: TEST_HARNESS -->
      <applicationSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</applicationSecret>
      <name>TEST_HARNESS</name>
    </SecurityApplication>
  </insert>
  <insert skipIfError="false" skipIfExists="true">
    <SecurityDevice xmlns="http://santedb.org/model">
      <id>6746d4a7-7522-4334-8299-ffda8ea73202</id>
      <!-- Secret: TEST_HARNESS -->
      <deviceSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</deviceSecret>
      <name>TEST_OTHER|TEST</name>
    </SecurityDevice>
  </insert>
</dataset>
```
{% endtab %}

{% tab title="SDBAC" %}
```
> application.add TEST_OTHER -s TEST_HARNESS
> device.add TEST_OTHER|TEST -s TEST_HARNESS
```
{% endtab %}
{% endtabs %}



## Patient Missing PID-3.4 With No Authority

Test harness sends ADT^A01 message where the CX.4 of the PID is missing.

```
MSH|^~\&|TEST_OTHER|TEST|CR1|MOH_CAAT|20141104174451||ADT^A01^ADT_A01| TEST-CR-01-10|P|2.3.1
EVN||20101020
PID|||RJ-438^^^&&||JOHNSTON^ROBERT^^^^^L|MURRAY^^^^^^L|19830205|M|||1220 Centennial Farm Road^^ELLIOTT^IA^51532||^PRN^PH^^^712^7670867||||||481-27-4185
PV1||I
```

### Expected Behaviour

* Receiver rejects the message with an AR or AE
* Response is ACK^A01
* Response version is 2.3.1
* MSA indicates that an assigning authority (PID-3-4) could not be resolved.

{% hint style="info" %}
If using MSH-8 security (i.e. not node authentication) you should ensure that the `MSH-8` value of the message sent from the test harness contains `TEST_HARNESS+TEST_HARNESS`
{% endhint %}

