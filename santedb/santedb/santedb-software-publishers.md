---
description: Verified Extension Publishing
---

# SanteDB Software Publishers

{% hint style="info" %}
This page is still evolving - check back later when the publisher program documentation is complete.
{% endhint %}

## What is a Publisher?

SanteDB requires all deployments, extensions, customizations, etc. be digitally signed by the a trusted certificate before the SanteDB server software will load and use the extension, screen, business rule, etc. 

Digital signatures ensure:

* The software you're loading into your SanteDB environment is authentic and has not been tampered with.
* The publisher of the extension/publisher is trusted by the SanteDB community and has been vetted.

When an extension or package has been vetted and signed, the applet will appear with a digital signature indicator:

![](../../.gitbook/assets/image%20%28404%29.png)

{% hint style="warning" %}
It is possible to disable the verified publisher status check on SanteDB software however this is not recommended as SanteDB will load any package files uploaded to it. 
{% endhint %}

## Becoming a Publisher

To become a SanteDB software publisher, we've implemented a relatively low overhead, while ensuring trusted publishers can reliably use and leverage the SanteDB platform.

### Collecting Necessary Documentation

SanteDB does not issue publisher certificates to anyone who asks for them, the community first considers the applicant's history, community participation, and ability to write software. You may be asked to provide the following information:

* The country/jurisdiction you're interested in leveraging SanteDB 
* The size of your company/group \(\# of developers, time in business, previous projects, etc.\)
* A publicly available website which describes your company/group/project
* Optionally validation that you are a legitimate business such as a Duns and Bradstreet DUNS Number \(example: [Fyfe Software Inc.](https://www.dnb.com/business-directory/company-profiles.fyfe_software_inc.3144e262d98ff713e0449fe7584d20fe.html)\), Google Business page, or other government registration 
* Your group has developers with an understanding of the SanteDB platform.

### Applying for Publisher Certificate

Once you've collected the appropriate documentation you will need to apply for a publisher certificate. To do this:

1. Contact the SanteSuite team at [info@santesuite.com](mailto:info@santesuite.com) including the documentation you have available above. You should send this request from an official e-mail \(i.e. not gmail or hotmail\) 
2. The SanteSuite team will schedule an interview with your group and will discuss your project and publisher requirements, how SanteSuite can provide assistance, etc. \(this interview also ensures the applicant is a real person\)
3. You will be invited to submit a CSR \(Certificate Signing Request\) , this is a process whereby your developers generate a private digital signature key and request SanteSuite Community sign it.

### Using your Publisher Certificate

When your group has completed the sign up process, you will receive an e-mail with your X509 code signing certificate, the SanteSuite Community Signing Certificate chain. You will have to [combine these ](https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/)with your private key to create a PKCS12 \(`.pfx`\) file. 

When packaging applets/extensions/etc. you will need to sign these applications, when packaging your applets:

```text
pakman --compile --source=./myapplet/ --output=./myapplet.pak --keyFile=mykey.pfx --embedcert
```

## Frequently Asked Questions

#### Do I need to be a registered publisher to use SanteDB?

No, you do not need a publisher certificate to run and/or operate SanteDB. You also do not need a publisher certificate to:

* Create custom data-sets
* Create custom matching configurations

#### Do I need to be a registered publisher to contribute to SanteDB projects?

No, you can freely develop, test, modify and change the SanteDB core applets \(and SanteMPI, SanteGuard, SanteEMR, etc.\) without a publisher certificate. You will simply not be able to publish your changes as though they are SanteSuite's \(i.e. you will need to initiate a pull request and SanteSuite will sign the changes when they are built into a release of the product\)

#### Do I need a publishing certificate to develop my own Applets?

No, you can run and develop applets without a publisher signing key. You will be limited to the SDK and iCDR/dCDR servers which have been configured to ignore unsigned packages.

#### How long to publisher certificates last?

Publisher certificates are issued depending on the project, the partner, and community guidelines. Certificates are issued usually for 365 days from issuance \(1 year\) however longer publisher certificates can be arranged upon request.

#### If my certificate expires, will my extensions still work?

Yes, your extensions are timestamped when they are packaged into an applet. Software can still be executed, however you will not be able to publish new versions.

#### How much does becoming a publisher cost?

There is currently no cost to becoming a SanteDB publisher, however if the demand for publishing certificates becomes a burden to the community, a nominal cost-recovery fee may be collected in the future to ensure sustainability  of the verified publisher programme.



