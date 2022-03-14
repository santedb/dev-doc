# Develop Operational Technology Architecture

An operational technology architecture differs slightly from a software requirements specification or functional design specification for software. The operational technology architecture is primarily concerned with the operational environment in which SanteDB services will be running.

## Writing your Operational Architecture Document

The documentation prepared for the operational architecture should aim to:

* Provide a high-level summary of how users interact with the system, and the purpose of the system (this is helpful for network and server operators to understand what types of operational issues may arise)
* Document the physical architecture of the servers, virtual machines, networks, etc. of the operational deployment
* Describe the disaster recovery options, backup requirements, and security environment (remote access requirements, etc.)
* Enumerate the IP addresses, host names, and network infrastructure of where components of the SanteDB software is operating
* Describe the business continuity plans&#x20;
* Describe how the SanteDB infrastructure integrates with other local systems (network addresses, data formats, type of data, etc.)
* Describe specific data configurations, concept sets, extensions, locations, etc. found in the country deployment.

### Summarize Software Environment

The operational architecture documentation should summarize the software environment in which the SanteDB server is being operationalized (in the example document, note the summarization of the software components).&#x20;

The operational documentation should keep discussion of software components and business processes to a brief overview (the majority of your software modifications and flows should be captured in a FDS).&#x20;

Consider, for example, the software architecture for the Demoland example. \


![](<../../../.gitbook/assets/image (432).png>)

You will note that the software summary is concerned about the overall deployment of the software components onto various server infrastructure, and illustrating how data is shared and flows between these components.

The operational architecture of your SanteDB deployment will be highly variable, based on the intended goals and current ground truth (availability of internet, local system capabilities, clinics, workflows, etc.)&#x20;

### Describe the Physical Environment

The operational architecture should describe the operational environment on which the SanteDB software solution will be running. It is convenient to just claim "we're running SaaS", but system administrators will need detailed descriptions of the physical environment.&#x20;

This description should include a server deployment diagram (see below for an example), or if using cloud services, how those services are deployed. If the solution is deployed in clinics with special software or hardware, those deployments should also be documented. The goal is the clearly illustrate how the software is deployed so the operators can maintain the system.

![](<../../../.gitbook/assets/image (450).png>)

Additionally, any hardware specifications or network specifications should be clearly enumerated in the operational documentation. This includes:

* The brand name of any equipment being used (example: Lenovo ThinkServer ST550) - this helps maintainers understand how to get support for the hardware.
* The configuration of the equipment including any options which were configured (example: 2x Intel Xeon Silver 4220 , 128 GB RAM, 1 PCIe nVME Boot Drive, 2x GBe NIC, etc.). This helps maintainers understand the scope and size of the deployment, as well as providing a concrete list of parts which can (or need) to be reordered in case of failure.
* The software environment of the physical equipment such as any operating systems, SIEM or APM software, antivirus configuration, etc. This helps maintainers understand the third party software in use in the operational deployment.

{% hint style="info" %}
The documentation samples refer to POSE and VOSE which is the Microsoft Licensing nomenclature for Physical Operating System Environment and Virtual Operating System Environment respectively.&#x20;
{% endhint %}

#### Sizing a Server Environment

The sizing of your physical environment will depend heavily on a variety of factors such as the use of the SanteDB product, whether offline mode is leveraged, how many users and systems are connecting to the system, etc.

As a general rule, when deploying SanteDB on a physical environment the iCDR components can be computed as:

| Component             | SIzing                               | Example                                                            |
| --------------------- | ------------------------------------ | ------------------------------------------------------------------ |
| iCDR Server CPU       | $$n_{vcpu} = \frac{n_{clients}}{4}$$ | 20 concurrent clients = 5 VCPU minimum                             |
| iCDR Server RAM       | 4GB - 8GB                            |                                                                    |
| PostgreSQL Server CPU | $$n_{vcpu} = icdr_{vcpu}* 2$$        | 5 VCPU on iCDR = 10 VCPU                                           |
| PostgreSQL RAM        | $$n_{ram}=n_{vcpu} * 512{MB}$$       | 10 VCPU = 5 GB RAM minimum (more is better to tune `max_work_mem`) |
| PostgreSQL Disk       | As fast as possible                  |                                                                    |

Additional hints for sizing a physical environment:

* Buy two of everything instead of one physical server, buy two smaller ones - this is beneficial because:
  * It provides load balancing opportunities
  * It provides a failover environment when the hardware fails
* Always purchase SSD or NVMe based storage for your database servers
* Always run your storage in a redundant mode (i.e. run in RAID1, RAID1+0, RAID5+0 or RAID6)
* Where possible use PostgreSQL streaming replication on the primary CDR database to balance queries and writes
* Where possible use a Storage Area Network with lots of IOPS for throughput
  * If using a SAN ensure the storage network is on a different NIC than other network traffic
  * A SAN allows hypervisors to ship VMs between hosts to balance load or to provide rapid failover (using VMotion)
* Always buy spare parts (disks, RAM, network cards, etc.) matching the configuration of the hardware in the original equipment (this provides quick replacement for failed hardware)

### Describe the Network Environment

Your operational documentation should describe the networking environment used in the deployment. This includes:

* IP addresses and host names of each POSE and VOSE in use in your deployment
* All ports which are opened on the operating system firewalls (if any) including their port number, protocol and type of data flowing through the port (including if they are secured or not)
* How load balancers, SSL termination, or application firewalls should be configured to handle traffic (example: external host `https://mpi.gov.demoland.com:8443` is routed to `http://mpi-prod:8080`)
* Any remote access ports or requirements which are opened. This could include SSH access points, Microsoft Remote Desktop, VNC, or even VPN settings which will be used to access the console or host operating systems.

### Describe Service Availability Requirements

SanteDB often acts as an integration point for many different systems and often plays vital roles in a health system. What happens, however, when that infrastructure is not available?

It is fact of life that servers fail, networks are unreachable, or other any other combination of issues can arise. The operational architecture should at least identify how this will impact business users. For each component in your deployment, the availability section should describe:

* The observed impact of an outage of the particular component (for example: what happens when the database server is offline)
* Mitigations that can be taken to recover or prevent the outage condition
* Descriptions of what the business impact of a component being absent would have on users (example: If the one of the SanteMPI host servers is unavailable, what impact would it have on users? What options are there to continue doing business?)

### Describe Service Contacts and Responsibilities

Large deployments often involve a large number of staff, companies, agencies and ministries. It is important that a clear set of responsibilities be established for each. This is important as it allows readers of the operational architecture to understand:

* Which partner in the deployment is responsible for which maintenance or corrective activities?
* What are the hours of operation (or expected availability) of each partner?
* What are the escalation procedures and tiers for supporting the deployment?

### Describe Business Continuity Procedures

When an issue is detected and impacts business users, they will often need to continue doing their work (even though the software is unavailable). Your operational architecture document should include a business continuity plan. The continuity plan should identify:

* What should users do when the system is unavailable? (go back to paper? replace devices? change sites? etc.)
* How should users report their issues when they experience an outage? (Is there a helpdesk? A bug tracker? etc.)
* What are the RPO, RTO and MTO values for the deployment? (see below)
* What are the procedures (for each component) to recover from a failure condition?

#### RPO, RTO and MTO

* Recovery Time Objective (RTO) – The maximum amount of time that could be tolerated between unexpected failure and the resumption of normal service. (i.e. How long can clinics operate without the system?). RTO dictates the goal for recovering the service operation.
* Recovery Point Objective (RPO) – The maximum period of time which data might be lost if service unexpectedly fails. (i.e. How far back can you fail without being a catastrophic loss to business?). RPO usually informs the frequency of your backups and impacts the cost of your backup infrastructure.
* Maximum Tolerable Outage (MTO) – The maximum amount of time that the business can tolerate complete cessation of the project during normal business days before it becomes impossible to continue doing work.

### Describe Update Procedures

Software is a living product and evolves over time and it is important to ensure that operating systems, clinical systems, antivirus software, firewalls, etc. are all updated to ensure that the latest security and features are present in the environment.

Typically updates require organizational planning to ensure that maintenance windows do not overlap with business operations, and that any special processes (like backups, snapshots, service stop/start, etc.) are done in a particular order.

The operational architecture should describe all of these impacts on the environment, as well as any special procedures that must be followed. For example:

> Prior to updating the SanteDB dCDR software in clinics, ensure:
>
> * The OpenMRS server is shut down and users logged out.
> * The SanteDB dCDR synchronization center indicates no conflicts and no remaining upload data (in the outbox)
> * The backup job is run to produce a recent copy of data in the dCDR
>
> &#x20;

### Describe the Security Environment

Your operational architecture document should describe the security environment which is being used in your deployment. This should include:

* When are new devices or applications integrated into the SanteDB infrastructure? What approvals are required and/or sign offs?
* When are new users added to the SanteDB infrastructure? What groups are they assigned to? What control do they have over the solution and hardware?
* What firewalls are in place and/or configured?
* How is data encrypted by integrated software solutions in transit between systems and at rest? (example: How are the HL7v2 messages encrypted between a Hospital Information System and the SanteDB iCDR?)
* How are systems authenticated? What are the policies in the deployment for password and account expiration?
* What are the custom policies applied or configured in the operational environment?

## Resources

The SanteDB team has prepared a template which may be helpful for organizing your Operational Architecture. The document contains instructions and a limited example of content for Demoland to get writers started in authoring operational architectures.

{% file src="../../../.gitbook/assets/Operational Architecture Template.docx" %}
