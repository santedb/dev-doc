# Operationalizing SanteDB

Operationalizing SanteDB (or any SanteDB solution) is not a trivial task, any large scale deployment of the solution requires planning and coordination between stakeholders. Implementers are encouraged to use a formal methodology for enterprise architecture (such as CMMI or TOGAF) to manage the operationalization of the MPI projects.

Because operationalization is specific to the problem domain, local jurisdiction, size requirements, etc. SanteDB provides high level tasks for deployment as a reference guide, and provides operational templates for use by implementers which may be of use.

The overall operationalization of a SanteDB service can be illustrated with 5 major activities.

![](<../../.gitbook/assets/image (438).png>)

## Information Gathering



## Planning

After the vision for your SanteDB deployment project has been established, and relevant stakeholders are on board, it is time to begin the planning phase of the SanteDB/SanteMPI solution. Depending on how the target context's project management office operates, the process may differ.&#x20;

See: [planning-and-preparation-work](planning-and-preparation-work/ "mention")

## Development / Integration

## Deployment

The deployment phase of SanteDB involves the installation, configuration, validation and testing of the environment.

See: [deployment](../installation-1/deployment/ "mention") for detailed information about deploying SanteDB software.

## &#x20;Rollout

Overall, the installation process can be described as:

1. Choose one of the appropriate [santedb-solutions.md](../../santedb/santedb-solutions.md "mention") for your use case.
2. Complete the necessary [planning-and-preparation-work](planning-and-preparation-work/ "mention")which includes:
   1. Establishing a master list requirements, of identity and data elements for your deployment.
      1. [configuring-identity-domains.md](../installation-1/planning-and-preparation-work/develop-an-information-architecture/configuring-identity-domains.md "mention")&#x20;
   2. Creating an operational deployment architecture document outlining the ports/servers/etc. your deployment will use.
   3. Performing a Threat Risk Assessment (TRA)&#x20;
   4. Performing a Privacy Impact Assessment (PIA)
   5. Preparing / Adapting Standard Operating Procedures (SOP) documents
   6. Preparing a master user list, a master role list and related governance policies
   7. Planning your budget for hardware, software licensing and services
   8. Acquiring and installing any server, network, hosting or pre-requisite software purchases
3. Install and configure your physical environment according to the Operational Deployment Architecture.
4. Install and configure the [santedb-server](../installation-1/deployment/software-deployment/santedb-server/ "mention")
5. [securing-the-apis.md](securing-the-apis.md "mention") using one of the documented methods
6. [installing-web-access-gateway.md](../installation-1/deployment/software-deployment/disconnected-gateway/installing-web-access-gateway.md "mention") to setup the [santedb-administration-panel](../../operations/cdr-administration/santedb-administration-panel/ "mention")
7. Complete the relevant configuration steps for your solution.
   1. If using SanteMPI:
      1. Perform the [fhir-interface-validation](../installation-1/deployment/software-deployment/santedb-server/installation-qualification/fhir-interface-validation/ "mention") to test your installation
      2. Configure your Data Access Policies
      3. Configure your Identity Domains
      4. Configure and Test your Match Configurations
8. Onboard any trading partners
