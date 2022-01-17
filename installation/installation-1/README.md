# Installing SanteDB

When installing SanteDB iCDR and dCDR instances on your environment, the process can be complex, and there are many variables which may impact the pattern you use to deploy the software for your project.&#x20;

## Installation for Development&#x20;

When installing SanteDB in a development environment, we recommend[docker-containers](santedb-server/installation-using-appliances/docker-containers/ "mention")for your iCDR instance and then [installing-the-dcdr-sdk.md](disconnected-gateway/installing-the-dcdr-sdk.md "mention").

You can then clone the start code and follow the [getting-started.md](../../developers/extending-santesuite/extending-santedb/applets/getting-started.md "mention") article to start developing SanteDB applications!

## Installation for Production

Overall, the installation process can be described as:

1. Choose one of the appropriate [santedb-solutions.md](../../santedb/santedb-solutions.md "mention") for your use case.
2. Complete the necessary [planning-and-preparation-work](planning-and-preparation-work/ "mention")which includes:
   1. Establishing a master list requirements, of identity and data elements for your deployment.&#x20;
   2. Creating an operational deployment architecture document outlining the ports/servers/etc. your deployment will use.
   3. Performing a Threat Risk Assessment (TRA)&#x20;
   4. Performing a Privacy Impact Assessment (PIA)
   5. Preparing / Adapting Standard Operating Procedures (SOP) documents
   6. Preparing a master user list, a master role list and related governance policies
   7. Planning your budget for hardware, software licensing and services
   8. Acquiring and installing any server, network, hosting or pre-requisite software purchases
3. Install and configure your physical environment according to the Operational Deployment Architecture.
4. Install and configure the [santedb-server](santedb-server/ "mention")
5. [securing-the-apis.md](../installation/securing-the-apis.md "mention") using one of the documented methods
6. [installing-web-access-gateway.md](disconnected-gateway/installing-web-access-gateway.md "mention") to setup the [santedb-administration-panel](../../operations/cdr-administration/santedb-administration-panel/ "mention")
7. Complete the relevant configuration steps for your solution.
   1. If using SanteMPI:
      1. Perform the [fhir-interface-validation](santedb-server/installation-qualification/fhir-interface-validation/ "mention") to test your installation
      2. Configure your Data Access Policies
      3. Configure your Identity Domains
      4. Configure and Test your Match Configurations
8. Onboard any trading partners
