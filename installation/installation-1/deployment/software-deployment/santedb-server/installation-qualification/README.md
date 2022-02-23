# Installation Qualification

After installing a SanteDB iCDR product, such as SanteMPI or SanteIMS, there is often a need to validate that the software is setup and functioning correctly. This page provides reference materials for running these installation qualification tests.

## Security / User Interface Testing

The Security Administration Testing wiki article provides test steps that users can perform to validate that the security environment of SanteDB is running correctly.&#x20;

If you're running the iCDR and the web host portal you can use the [User Interface Test Cases ](security-administration-testing/test-cases-for-ui-1/), if you're operating SanteDB iCDR in a headless environment the [Admin Console tests](broken-reference) provide equivalent tests using the `sdbac` tooling.

## SanteMPI Functional Testing

If you've installed the SanteMPI solution you can use the [Master Patient Index / Client Registry](fhir-interface-validation/) test cases to validate your configuration of SanteMPI.

The test cases cover:

* [HL7 FHIR Test Cases ](fhir-interface-validation/mpi-cr-test-cases-for-fhir/)
* [HL7 Version 2 Test Cases](fhir-interface-validation/mpi-cr-test-cases-for-hl7v2/)

{% hint style="info" %}
It is important that you use the default configurations for SanteMPI when running these tests. Changes in configuration should be performed after the qualification testing is completed. This applies to:

* Matching Configuration Changes
* Queueing or Dispatching Changes
* Pub-Sub Behavior Changes
{% endhint %}

