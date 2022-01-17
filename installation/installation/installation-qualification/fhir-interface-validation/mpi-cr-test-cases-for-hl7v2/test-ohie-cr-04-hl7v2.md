---
description: Patient Identity Feed – Blocks invalid assigning authority
---

# TEST: OHIE-CR-04-HL7v2

This test ensures that two sources cannot assign identifiers from the other’s assigning domain. In this test, the harness mimics two authorities (TEST\_HARNESS\_A and TEST\_HARNESS\_B). They each register a patient and the harness then verifies that TEST\_HARNESS\_B does not assign an identifier from TEST\_HARNESS\_A’s identity domain.

## Discussion

While not a hard requirement of the IHE Patient Identity Cross Referencing specification, it is important to ensure that identity sources are governed in a manner which ensures that cross-domain registrations/merges/modifications are performed.&#x20;

[IHE ITI-8 TF Vol 2a](https://profiles.ihe.net/ITI/TF/Volume2/ITI-8.html) indicates that the association of identity sources with their assigning authority be a supported feature, particularly in section 3.8.4.1.3.1:

> Patient Identity Source for the domain. This is expected to be the MSH-3 Sending Application and the corresponding MSH-4 Sending Facility fields in the HL7 ADT message. (Alternative identification schemes might include IP address of the Patient Identity Source or Node Authentication if the Audit Trail and Node Authentication Integration Profile is used.)

{% hint style="info" %}
This test represents a test of the ability of the client registry to perform basic governance of data submissions. This test case may not be a requirement in all jurisdictions.&#x20;
{% endhint %}

## Pre-Conditions / Setup

Prior to executing the tests in this test case, the system under test should be configured such that:

* Application `TEST_HARNESS_A` is configured
* Application `TEST_HARNESS_B` is configured
* Device `TEST_HARNESS_A|TEST` is configured&#x20;
* Device `TEST_HARNESS_B|TEST` is configured
* Authority `TEST_A` with OID `2.16.840.1.113883.3.72.5.9.2` is configured and `TEST_HARNESS_A` is granted authority to assign identifiers in this domain
* Authority `TEST_B` with OID `2.16.840.1.113883.3.72.5.9.3` is configured and `TEST_HARNESS_B` is granted authority to assign identifiers in this domain.

{% tabs %}
{% tab title="Dataset" %}
```markup
<dataset id="Test Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <insert skipIfError="false" skipIfExists="true">
    <SecurityApplication xmlns="http://santedb.org/model">
      <id>DE5BEC1E-8C41-4FF1-8E65-A39AC1DDAE60</id>
      <!-- Secret: TEST_HARNESS -->
      <applicationSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</applicationSecret>
      <name>TEST_HARNESS_A</name>
    </SecurityApplication>
  </insert>
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE TEST Domain A</name>
      <domainName>TEST_A</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.2</oid>
      <url>http://ohie.org/test/test_a</url>
      <isUnique>true</isUnique>
      <assigningApplication>DE5BEC1E-8C41-4FF1-8E65-A39AC1DDAE60</assigningApplication>
    </AssigningAuthority>
  </insert>
  <insert skipIfError="false" skipIfExists="true">
    <SecurityApplication xmlns="http://santedb.org/model">
      <id>58275680-5129-4832-9668-131F76E8DFB6</id>
      <!-- Secret: TEST_HARNESS -->
      <applicationSecret>b5547020757c0efa3f320fbd2a0c43d0628e19b8cd81652523b87d31fc54f5ec</applicationSecret>
      <name>TEST_HARNESS_FHIR_B</name>
    </SecurityApplication>
  </insert>
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE TEST Domain B</name>
      <domainName>TEST_B</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.3</oid>
      <url>http://ohie.org/test/test_b</url>
      <isUnique>true</isUnique>
      <assigningApplication>58275680-5129-4832-9668-131F76E8DFB6</assigningApplication>
    </AssigningAuthority>
  </insert>
  
```
{% endtab %}

{% tab title="SDBAC" %}
```
> application.add TEST_HARNESS_A -s TEST_HARNESS
> device.add TEST_HARNESS_A|TEST -s TEST_HARNESS
> aa.add -n TEST_A -o 2.16.840.1.113883.3.72.5.9.2 -u http://ohie.org/test/test_a -d 'OpenHIE Test Domain A' -a TEST_HARNESS_A
> application.add TEST_HARNESS_B -s TEST_HARNESS
> device.add TEST_HARNESS_B|TEST -s TEST_HARNESS
> aa.add -n TEST_B -o 2.16.840.1.113883.3.72.5.9.3 -u http://ohie.org/test/test_b -d 'OpenHIE Test Domain B' -a TEST_HARNESS_B
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If the SanteMPI instance is configured to use Msh8 security and not node authentication, then the `MSH-8` value of all test messages must contain `TEST_HARNESS+TEST_HARNESS`
{% endhint %}

## Register Patient in TEST\_A

Test harness (as `TEST_HARNESS_A`) sends `ADT^A01` registering a new patient with an identifier from `TEST_A` domain.

```
MSH|^~\&|TEST_HARNESS_A^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-04-20|P|2.3.1
EVN||20101020
PID|||RJ-439^^^TEST_A||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an `AA`
* MSH-5 and MSH-6 matches `TEST_HARNESS_A|TEST`
* Response is `ACK^A01`
* Response version is `2.3.1`

## Cross-Domain Registration in TEST\_A

Test harness (as `TEST_HARNESS_B`) attempts to send an `ADT^A01` for authority A.

```
MSH|^~\&|TEST_HARNESS_B^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-04-30|P|2.3.1
EVN||20101020
PID|||NFD-3049542-23^^^TEST_A||JONES^JENNIFER^^^^^L|SMITH^^^^^^L|19840125|F|||123 Main Street West ^^NEWARK^NJ^30293||^PRN^PH^^^409^30495||||||
PV1||I
```

### Expected Behaviour

* Receiver rejects the message with an `AE` or `AR`
* An MSA message exists with an appropriate error code
* `MSH-5` and `MSH-6` matches `TEST_HARNESS_B|TEST`
* Response is `ACK^A01`
* Response Version is 2.3.1
