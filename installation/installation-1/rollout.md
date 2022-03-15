# Rollout

The rollout phase of your project occurs after the deployment has been completed. Typically a rollout will involve context specific activities (for the clinical domain, the deployment pattern, etc.).&#x20;

The implementation of even a transparent data sharing project (like SanteMPI) can represent a shift in the thinking for users who previously may have not had to worry about sharing, privacy and security of data in their context.&#x20;

## Pre-Flight Checklist

* [ ] [SanteDB Deployment Completed](deployment/)
  * [ ] Physical & Virtual Environment Installed & Documented
  * [ ] iCDR Environment (SanteMPI, SanteDB, etc.) installed
  * [ ] [Relevant Installation Qualification Completed](deployment/installing-software/santedb-server/installation-qualification/)
  * [ ] [Services Properly Tuned & Configured](../installation/santedb-server/production-installation-notes.md)
  * [ ] [APIs Secured](deployment/securing-the-apis.md)&#x20;
* [ ] [Privacy Impact Assessment Performed](planning-and-preparation-work/developing-privacy-impact-assessments.md) on iCDR
* [ ] [Threat/Risk Assessment Performed](planning-and-preparation-work/develop-threat-risk-assessments.md) on iCDR

## Establish a Help / Support Desk

No software environment is perfect. When deploying large scale systems many users will encounter issues which need to be documented and resolved in a coherent manner. For example:

* Users forget their passwords or require assistance logging into the solution,&#x20;
* Hardware (tablets, laptops, routers, etc.) breaks and needs to be replaced,
* Users forget a procedure or process or require assistance to complete a workflow.

It is recommended that, during rollout, the establishment of an operational help desk and ticketing software is created. This should reference the [#describe-service-contacts-and-responsibilities](planning-and-preparation-work/develop-operational-technology-architecture.md#describe-service-contacts-and-responsibilities "mention") documentation developed for the project. As a rule of thumb, for every 75 to 100 terminals/clients/users a single IT support resource should be available (note: support staff can be a power user, clinic representative, IT operations staff already servicing a location, etc.)

## Creating Job Aides & SOPs

During the rollout of the SanteDB software, it is important that all users of the system follow common procedures and have ready access to assistance. This will help ensure the consistency of data captured and shared via SanteDB, adherence to privacy and security best practices, documentation requirements, etc.

Useful assets which should be developed include:

* Clinical Job Aides: For clerks, clinicians, nurses, community health workers, etc. which document the business processes to be followed by users of the SanteDB system. These should be short (less than a page) guides for common tasks which users can reference.
* Video Training Tutorials: Illustrating the workflows and standard operating procedures in use in the country or context. These can either leverage the SanteSuite community channel video content or can be created (for example: if your jurisdiction is using OpenMRS you would develop OpenMRS videos)
* Standard Operating Procedures:  SanteSuite provides generic [standard-operating-procedures](../../operations/standard-operating-procedures/ "mention") and a [standard-operating-procedure-template.md](../../operations/standard-operating-procedures/standard-operating-procedure-template.md "mention") which can be used by implementers to document their own SOPs. SOPs are useful for documenting official procedures for the SanteDB deployment. &#x20;

## Assessing Clinics & Sites

When onboarding new clinics or sites which are using the dCDR technology, or when onboarding new trading partners it is important to perform an assessment.

It may seem benign, however, onboarding a software product or site which is not accustomed to sharing PHI can be quite a shift in thinking.&#x20;

* Users may need to alter their workflows for patient registration or data capture to implement best practices for ensuring data shared with a central level is accurate,
* Users may need to capture additional details about patients or events which they have not needed to capture before,&#x20;
* Users need to be informed of the privacy and security practices for sharing of discrete patient records,
* Users will need to be familiarized with standard processes and workflows so that cross-site data capture is consistent.

Additionally, from a technical standpoint, highly sensitive and confidential data is being disclosed and stored between sites. This requires updates to the local operating environments to ensure that an attempt is made to protect the data.&#x20;

Additionally, when onboarding new sites which will share discrete data with a central system or other clinics, it is important that there patients are informed as well. This may include:

* Producing or sharing informational posters or notices about the sharing of personal health information,
* Creating brochures which inform patients of the type of data being capture, and the intended use of the data sharing,
* Creating processes to document patient consent to participate and familiarization with consent is important for clinicians and patients (example: care won't be denied for refusal of consent)

SanteSuite has prepared an assessment toolkit resource which can be adapted by implementing partners to assess clinical settings, software, or organizations which will be integrating with the SanteDB infrastructure.

{% file src="../../.gitbook/assets/MPI Readiness Assessment.docx" %}

## Training and Knowledge Dissemination

Once a site has been properly secured to meet local requirements, the clinic staff should be trained on the new processes, data elements, and the project.&#x20;

A useful strategy to scale this training and knowledge transfer is the Training of Trainers (ToT) pattern. In this pattern, a small group of "champions" are trained. These trainers should be comfortable:

* Explaining the purpose of the project (the vision)
* Explaining the new business processes or modified business processes for clinic staff
* Disseminating the Standard Operating Procedures for the SanteDB context
* Installing and configuring any required software on local devices required

The method of performing the ToT/site rollout will depend on your context, the clinical domain, the use of dCDR or iCDR assets, etc. SanteSuite has had success in performing two-day rollouts where:

* Day 1 Activities - Training & Installation&#x20;
  * Any software or configurations required are installed and activated in the clinic site
  * Connectivity to the central training or staging system are validated
  * Clinic staff are familiarized with the relevant platform components (new screens, common error conditions)
  * Clinic staff are familiarized with any new business processes, minimum data sets, or procedures in their role
  * Clinic staff participate in basic privacy and security training (phishing, safe browsing, informed consent, etc.)
  * Clinic staff use the testing/training system to become familiar with the software
  * Clinic staff are familiarized with the ticketing / helpdesk solutions and how to raise issues.
* Day 2 Activities  - Normalization, Observation & Assistance
  * Clinic staff use the production system in their day-to-day work with real patients
  * Trained Trainers observe the use of the system and the adherence to the new processes and policies, providing input and guidance when needed
