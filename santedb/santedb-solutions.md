# SanteDB Solutions

The SanteDB Clinical Data Repository (CDR) is designed for large-scale regional/national applications running on SanteDB may be deployed in dozens, hundreds or evens thousands of clinics across a region. In these scenarios, there will be times where individual clinics or points of service will lose connectivity, and this is especially true in geographically sparse or low resource environments. SanteDB was designed from the ground up to support this highly distributed scenario, and is equipped with a robust synchronization engine that allows individual clinics to go online and offline as they require, while allowing users to continue work in their applications without being uninterrupted and without losing any clinical data. When clinics are able to re-establish connectivity, all transactions are synchronized seamlessly between local data stores and the central repository. Each remotely deployed application instance (in a clinic or "out on the field") maintains a local version of SanteDB referred to as the distributed clinical data repository or "dCDR". The main central clinical data repository is referred to as the iCDR.  &#x20;

SanteDB solutions run on top of the CDR and are pre-configured, pre-packaged plugins which modify SanteDB and extend it to provide a solution to a clinical problem. SanteDB has several solutions targeted to individual clinical domains and use cases, including national health identifiers, master patient index/client registry solutions, national immunization planning and tracking solutions, a distributed EMR and more. The following diagram illustrates how applications make use of SanteDB by extending the base functionality of the SanteDB Core:&#x20;

![](<../.gitbook/assets/image (188).png>)

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
