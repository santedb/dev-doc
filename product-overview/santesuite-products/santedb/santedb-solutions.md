# SanteDB Solutions

The SanteDB CDR (both the iCDR and dCDR) are an online/offline clinical data repository software solution. However, the ability of a software solution to store/retrieve data and secure often times provides little benefits as they provide a high barrier for implementers to realize clinical workflows.

SanteDB solutions are pre-configured, pre-packaged plugins which modify SanteDB and extend it to provide a solution to a clinical problem. SanteDB has several solutions targeted to individual clinical domains and use cases.&#x20;

![](<../../../.gitbook/assets/image (188).png>)

* **SanteGuard** : The SanteGuard solution is a complete audit repository solution. The SanteGuard solution contains:
  * .NET Based Plugins for the SanteDB dCDR and iCDR which allow SanteDB to accept IHE ATNA messages.
  * Applet Widgets which extend the other SanteDB solution user interfaces to add detailed auditing information for system administrators.
  * Extended data storage schemas and plugins to store information related to audit log review workflows.
* **SanteEMR** : The SanteEMR solution is a framework which provides basic EMR functionality such as scheduling, registration, patient management, clinical templates, etc. Included:
  * Patient Registration and Search Management Workflows
  * Clinical Templates for birth, death, and basic primary care events.
* **SanteIMS** : The SanteIMS solution provides extended user interfaces and clinical protocol support related specifically to immunizaiton clinics. Included in SanteIMS:
  * Stock management functionality including adjustments, current balances, and order/fulfillment
  * Pre-built clinical decision support related to immunization activities.
* **SanteMPI** : The SanteMPI solution provides a combination of pre-configured plugins for the SanteDB CDR to work as an MPI. Inlcuded:
  * .NET based plugins which modify the behavior of the HL7v2 and FHIR interfaces to implement IHE PIX, PDQ constraints.
  * Plugins for name aliasing&#x20;

These solutions provide a basis for community extensions to create branded versions of the underlying applications.
