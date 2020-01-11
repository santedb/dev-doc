---
description: >-
  This page describes the planning and preparation work that must be undertaken
  prior to installing SanteDB in a production environment.
---

# Planning & Preparation Work

A SanteDB deployment is not like installing Microsoft Office, or a video game. SanteDB is responsible for storing very sensitive personal health information \(PHI\) and the deployment of SanteDB in any role \(MPI, MFR, MPR, SHR, etc.\) warrants careful planning and consideration. 

{% hint style="info" %}
It is recommended that you reach out the SanteSuite community prior to performing a deployment of any SanteSuite product. Our partners can assist with planning and deployment services.
{% endhint %}

### Plan SanteDB's Role in your Architecture

SanteDB is a generic CDR, it can operate as a Master Patient Index, a Shared Health Record, an Immunization Repository, etc. You should understand which role\(s\) you want SanteDB to play in your infrastructure prior to deploying it. Some questions to consider:

* How does this system fit into my national eHealth Blueprint? 
* Does my environment require offline access to data, or only online access to data?
* What is the scope of data that SanteDB will be storing? \(patients, facilities, providers, health records, etc.\)
* Do I need SanteDB to operate in single instance storage mode, or multi-instance storage mode?
* What types of matching/merging of data will be needed?
* What is the technical capacity in my jurisdiction? Do we already have tablets? Laptops? Servers?
* What other types of systems exist in my jurisdiction? Will SanteDB need to integrate with any of them? Which standards do they support?
* Which systems do I want to connect to SanteDB? Which standards do those systems support?
* What is the size and velocity of data storage which SanteDB will be encountering? How many new records are added to the system each year?
* Will there be a need for custom screens in your deployment or will you be using the default SanteDB community interfaces?

### Plan your Privacy & Security Architecture

SanteDB has a very robust privacy and security architecture. It supports everything from simple on/off blocking, to complex rules around access controls and elevation of user principals. Some questions to consider:

* Have you appointed an accountable person, who will be in charge of ensuring your local laws surrounding patient confidentiality / privacy are implemented properly?
* Have you performed a Threat Risk Assessment for your deployment environment? 
* Have you performed a Privacy Impact Assessment for your deployment environment?
* Do you have a security certificate obtained from a valid certificate authority?
* Do you have a applet signing key obtained from the SanteDB community? \(this is required to write custom applets\)
* What types of data / events will I need to audit? What is my audit retention policy?
* What are my user account policies? How will I issue new user accounts?
* What are my device and application policies? How will I onboard new applications and devices?



