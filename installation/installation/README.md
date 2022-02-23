# Operationalizing SanteDB

Operationalizing SanteDB (or any SanteDB solution) is not a trivial task, any large scale deployment of the solution requires planning and coordination between stakeholders. Implementers are encouraged to use a formal methodology for enterprise architecture (such as CMMI or TOGAF) to manage the operationalization of the MPI projects.

Because operationalization is specific to the problem domain, local jurisdiction, size requirements, etc. SanteDB provides high level tasks for deployment as a reference guide, and provides operational templates for use by implementers which may be of use.

The overall operationalization of a SanteDB service can be illustrated with 5 major activities.

![](<../../.gitbook/assets/image (438).png>)

## Information Gathering

The first step to deploying SanteDB solutions is to gather information about problem domain and jurisdiction in which the solution will be deployed. Activities may include

### Identify Stakeholders

Identify the people and organizations within the implementation context. Stakeholders include:

1. Relevant department(s) of the organization
2. Vendors of existing software solutions within the context
3. Subject matter experts for the problem domain, relevant standards and SanteDB products
4. Owners / Operators of health solutions (such as funders, NGOs, hospitals, etc.)

### Establish a Vision

Identify the reason why SanteDB or a SanteDB solution is needed in the context, and what clinical problem is being solved. It is helpful to indicate:

1. What problems are being solved?
2. Why do we need to solve them?
3. What are the timelines in which a solution should/needs to be found?

### Establish a Team

Identify a team of people who will be responsible for the process of operationalizing SanteDB in the context. The team which is identified/established ad their roles/responsibilities on the team will be highly variable (based on project).

SanteDB has had some success using the RACI methodology ([https://en.wikipedia.org/wiki/Responsibility\_assignment\_matrix](https://en.wikipedia.org/wiki/Responsibility\_assignment\_matrix)) which identifies team members who are:

* **R**esponsible - Completes the tasks or work described&#x20;
* **A**ccountable - Answerable to the project owner/sponsor for the accurate and thorough delivery of the work
* **C**onsulted - Subject matter experts or other persons/groups whose opinions are sought
* **I**nformed - Receives updates on progress (typically one way communication)

RACI charts are often defined using deliverables/tasks as rows and an organizational chart as columns. This makes it easy for project team members to know what their obligations are for each phase of the project delivery.

{% hint style="info" %}
The SanteSuite community cannot provide concrete RACI templates since they are highly variable based on roles of team members. However, we have provided a minimal template which may be of use to implementing partners.
{% endhint %}

{% file src="../../.gitbook/assets/RACI Worksheet.docx" %}

### Perform Environmental Scan

Engage with relevant stakeholders to perform an environmental scan of the current environment in which the SanteDB system is being deployed. It is important to observe/collect:

1. &#x20;Which systems are being used in the context?
2. What types of data do those systems collect?
3. What are the processes used by those systems and their users?
4. What are the operational difficulties that are being encountered? (lack of data, timeliness of access, etc.)
5. How are users authenticated or identified?&#x20;
6. What non-technical (business) processes are enforced?&#x20;
7. Perform Policy / Legislative Scan - Identify, collect, and document the relevant legal statutes, policies, laws, culture norms, etc. which may impact the project.&#x20;

## Planning

After the vision for your SanteDB deployment project has been established, and relevant stakeholders are on board, it is time to begin the planning phase of the SanteDB/SanteMPI solution. Depending on how the target context's project management office operates, the process may differ.&#x20;

See: [planning-and-preparation-work](planning-and-preparation-work/ "mention")

## Development / Integration

## Deployment

The deployment phase of SanteDB involves the installation, configuration, validation and testing of the environment.&#x20;

#### Finalize Operational Architecture

Before running `setup.exe` for the SanteDB solution, it is important to perform due diligence and plan the deployment.&#x20;

### Install Physical & Virtual Infrastructure



### Validate Operational Environment



### Document As-Deployed Environment

## &#x20;Rollout

Overall, the installation process can be described as:

1. Choose one of the appropriate [santedb-solutions.md](../../santedb/santedb-solutions.md "mention") for your use case.
2. Complete the necessary [planning-and-preparation-work](planning-and-preparation-work/ "mention")which includes:
   1. Establishing a master list requirements, of identity and data elements for your deployment.
      1. [configuring-identity-domains.md](../installation-1/planning-and-preparation-work/developing-an-information-architecture/configuring-identity-domains.md "mention")&#x20;
   2. Creating an operational deployment architecture document outlining the ports/servers/etc. your deployment will use.
   3. Performing a Threat Risk Assessment (TRA)&#x20;
   4. Performing a Privacy Impact Assessment (PIA)
   5. Preparing / Adapting Standard Operating Procedures (SOP) documents
   6. Preparing a master user list, a master role list and related governance policies
   7. Planning your budget for hardware, software licensing and services
   8. Acquiring and installing any server, network, hosting or pre-requisite software purchases
3. Install and configure your physical environment according to the Operational Deployment Architecture.
4. Install and configure the [santedb-server](santedb-server/ "mention")
5. [securing-the-apis.md](securing-the-apis.md "mention") using one of the documented methods
6. [installing-web-access-gateway.md](disconnected-gateway/installing-web-access-gateway.md "mention") to setup the [santedb-administration-panel](../../operations/cdr-administration/santedb-administration-panel/ "mention")
7. Complete the relevant configuration steps for your solution.
   1. If using SanteMPI:
      1. Perform the [fhir-interface-validation](installation-qualification/fhir-interface-validation/ "mention") to test your installation
      2. Configure your Data Access Policies
      3. Configure your Identity Domains
      4. Configure and Test your Match Configurations
8. Onboard any trading partners
