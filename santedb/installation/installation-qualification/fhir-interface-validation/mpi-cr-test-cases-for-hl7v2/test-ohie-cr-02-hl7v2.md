---
description: Patient Identity Feed – Auto-fill CX.4 data
---

# TEST: OHIE-CR-02-HL7v2

This test validates that the Client Registry is capable of populating the CX.4.1 from CX.4.2 and CX.4.3 or vice-versa given partial data in the CX.4 field. If configured to allow auto-resolution, then the authority of a message missing CX.4 should be assigned.

## Discussion

The primary basis for this test case is based in the nots for implementing ITI-8 \(Patient Identity Feed\) from the [IHE Technical Framework Vol 2a](https://profiles.ihe.net/ITI/TF/Volume2/ITI-8.html), specifically section `3.8.4.1.3`:

> If the PID-3.4 \(assigning authority\) component is not included in the message \(as described in Section 3.8.4.1.2.3\) the Patient Identifier Cross-reference Manager shall fill PID-3.4 prior to storing the ID information and performing its cross-referencing activities. The information filled by the Patient Identifier Cross-reference Manager is based on the configuration associating each of the Patient Identity Source Actors with the subcomponents of the correct assigning authority \(namespace ID, UID and UID type\). \(See Section 3.8.4.1.3.1 below for a list of required Patient Identifier Cross-reference Manager configuration parameters\).

The cases which are tested in this test are:

* The client registry can cross reference PID-3-4-1 with PID-3-4-2 and PID-3-4-3 data
* Conversely, the client registry can cross reference PID-3-4-2 and PID-3-4-3 with PID-3-4-1
* The client registry, when configured, can auto-resolve PID-3-4 when it is missing.

## Pre-Conditions / Setup

Prior to executing this test, SanteMPI instances should configure: 

* The `TEST_HARNESS` application
* The `TEST_HARNESS|TEST` device
* The `TEST` identity domain is created and the authority to assign is set to `TEST_HARNESS`
* The SanteMPI instance is configured such that `strictCx4` is disabled

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
      <id>508d9d71-54a3-4d67-897a-e2a395961395</id>
      <!-- Secret: TEST_HARNESS -->
      <deviceSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</deviceSecret>
      <name>TEST_HARNESS|TEST</name>
    </SecurityDevice>
  </insert>
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE TEST Domain</name>
      <domainName>TEST</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.1</oid>
      <url>http://ohie.org/test/test</url>
      <isUnique>true</isUnique>
      <assigningApplication>F0FC4322-948D-4986-A06C-DA603A77EDDE</assigningApplication>
    </AssigningAuthority>
  </insert>
```
{% endtab %}

{% tab title="SDBAC" %}
```text
> application.add TEST_HARNESS -s TEST_HARNESS
> device.add TEST_HARNESS|TEST -s TEST_HARNESS
> application.info TEST_HARNESS
> aa.add -n TEST -o 2.16.840.1.113883.3.72.5.9.1 -u http://ohie.org/test/test -d 'OpenHIE Test Domain' -a TEST_HARNESS 
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If the SanteMPI instance is configured to use Msh8 security and not node authentication, then the `MSH-8` value of all test messages must contain `TEST_HARNESS|TEST_HARNESS`
{% endhint %}

## Register Patient with CX.4.2 and CX.4.3

Test harness sends ADT^A01 message where the CX.4.1 of the PID is missing but the message contains CX.4.2 and CX.4.3. The client registry should use the information in the registration of the authority to fill the other components on the validation step of this test. 

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20141104174451||ADT^A01^ADT_A01|TEST-CR-02-10|P|2.3.1
EVN||20101020
PID|||RJ-438^^^&2.16.840.1.113883.3.72.5.9.1&ISO||JOHNSTON^ROBERT^^^^^L|MURRAY^^^^^^L|19830205|M|||1220 Centennial Farm Road^^ELLIOTT^IA^51532||^PRN^PH^^^712^7670867||||||481-27-4185
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* Response is ACK^A01
* Response is version 2.3.1
* MSH-5 and MSH-6 matches `TEST_HARNESS|TEST`

## Validate Auto-Fill of CX.1

Test harness ensures that patient was registered and receiver has populated CX.4.1 from the CX.4.2 and CX.4.3 values executing.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-02-20|P|2.5
QPD|IHE PIX Query|Q0220|RJ-438^^^&2.16.840.1.113883.3.72.5.9.1&ISO^PI
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an `AA`
* Response is `RSP^K23`
* Response message contains exactly one PID segment
* `PID-3` of PID segment contains an identifier having:
  * `PID.3.4.1` = TEST
  * `PID.3.4.2` = 2.16.840.1.113883.3.72.5.9.1
  * `PID.3.4.3` = ISO

## Register Patient with CX.4.1

Test harness sends ADT^A01 message where the CX.4.2 and CX.4.3 of the PID are missing but the message contains CX.4.1

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20141104174451||ADT^A01^ADT_A01|TEST-CR-02-30|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches `TEST_HARNESS|TEST`

## Validate Patient with CX.4.2 and CX.4.3

Test harness ensures patient was registered and receiver has populated CX.4.2 and CX.4.3 from the CX.4.1 value provided by executing:

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-02-40|P|2.5
QPD|IHE PIX Query|Q0220|RJ-439^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an AA
* Response message contains exactly one PID segment
* PID-3 of PID segment contains an identifier having:
  * `PID.3.4.1` = TEST
  * `PID.3.4.2` = 2.16.840.1.113883.3.72.5.9.1
  * `PID.3.4.3` = ISO

## Register Patient with no CX.4

The test harness sends a patient registration request with no CX.4 populated. Since `TEST_HARNESS|TEST` is configured to be the only assigner of `TEST` the client registry must fill the missing components of CX.4.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20141104174451||ADT^A01^ADT_A01|TEST-CR-02-30|P|2.3.1
EVN||20101020
PID|||RJ-499^^^TEST||JONES^ROBERT^^^^^L|BUKOWSKI^^^^^^L|19390125|F|||123 Main Street East^^NEWARK^NJ^30293||^PRN^PH^^^409^0394938||||||
PV1||I
```

### Expected Behaviour

* Receiver accepts message with an `AA`
* MSH-5 and MSH-6 contain `TEST_HARNESS|TEST`

## Validate Auto-Fill of CX.4

Test harness ensures that the patient was registered on client registry an CX.4 is populated based on the sender.

```text
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090223144546||QBP^Q23^QBP_Q21|TEST-CR-02-40|P|2.5
QPD|IHE PIX Query|Q0220|RJ-499^^^TEST^PI
RCP|I
```

### Expected Behaviour

* Receiver Accepts message with an AA
* Response message contains exactly one PID segment
* PID-3 of PID segment contains an identifier having:
  * `PID.3.4.1` = TEST
  * `PID.3.4.2` = 2.16.840.1.113883.3.72.5.9.1
  * `PID.3.4.3` = ISO

