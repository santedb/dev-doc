# Installation Qualification

After installing a SanteDB iCDR product, such as SanteMPI or SanteIMS, there is often a need to validate that the software is setup and functioning correctly. This page provides reference materials for running these installation qualification tests.

## User Interface Testing

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

## Security Environment Qualification

It is recommended that, after [securing-the-apis.md](../../../securing-the-apis.md "mention") is performed that a complete network scan be performed to ensure that the attack surface area of the environment is minimal.

* [ ] Perform a security scan of the applications involved (see: [OWASP ZAP](https://www.zaproxy.org/download/)) to ensure SSL, XSS, CORS, and other web security practices have been configured appropriately
  * [ ] Add any blocking scripts to browser headers your Application Firewall may be adding
  * [ ] Ensure proper caching policies and login policies are in place



* [ ] Perform a network port scan/attach tool to ensure that opened ports and services are minimal (see: [NMAP](https://nmap.org/))
  * [ ] Ensure that only ports you want opened are open
  * [ ] Ensure that ports that are open are secured.

![](<../../../../../../.gitbook/assets/image (555).png>)

* [ ] Use OpenSSL to validate that your SSL certificates are properly configured

```
openssl s_client -connect demompi.santesuite.net:443 -showcerts
CONNECTED(00000003)
depth=2 C = BE, O = GlobalSign nv-sa, OU = Root CA, CN = GlobalSign Root CA
verify return:1
depth=1 C = BE, O = GlobalSign nv-sa, CN = AlphaSSL CA - SHA256 - G2
verify return:1
depth=0 CN = *.santesuite.net
verify return:1
---
Certificate chain
 0 s:CN = *.santesuite.net
   i:C = BE, O = GlobalSign nv-sa, CN = AlphaSSL CA - SHA256 - G2
```
