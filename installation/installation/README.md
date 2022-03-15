# Operationalizing SanteDB

Operationalizing SanteDB (or any SanteDB solution) is not a trivial task, any large scale deployment of the solution requires planning and coordination between stakeholders. Implementers are encouraged to use formal methodologies for enterprise projects and architecture (examples: [CMMI](https://www.pmi.org/learning/library/cmmi-bring-pm-process-next-level-7538) , [TOGAF](https://www.opengroup.org/togaf), [DAD](https://www.pmi.org/disciplined-agile/process/introduction-to-dad), etc.) to manage the operationalization of the MPI projects.

Because operationalization is specific to the problem domain, local jurisdiction, size requirements, and other factors, the SanteDB wiki merely provides high level activities for operationalization as a reference. Any of the articles or templates found on the SanteSuite wiki are expected to be adapted by implementers, or to provide SanteDB specific considerations within their existing project management methodology.

The overall operationalization of a SanteDB service can be illustrated with 5 major activities.

![](<../../.gitbook/assets/image (438).png>)

{% hint style="info" %}
This guide is intended to supplement internal project management procedures and activities of the implementing organization. The sections focus primarily on the SanteDB specific aspects of project planning and analysis. Templates, worksheets, and other toolkits are provided on an as-is basis and should be adapted for appropriateness in the local context into which SanteDB is being deployed.
{% endhint %}

## Information Gathering

Many implementations don't start with a concrete idea of what the deployment of SanteDB will be achieving beyond "we need X". The information gathering phase of an operationalization project is intended to establish a concrete consensus among stakeholder of **what** the SanteDB CDR will be used for.

See: [information-gathering-and-analysis.md](../installation-1/information-gathering-and-analysis.md "mention")

## Planning

After the vision for your SanteDB deployment project has been established, and relevant stakeholders are on board, it is time to begin the planning phase of the SanteDB/SanteMPI solution. Depending on how the target context's project management office operates, the process may differ.&#x20;

See: [planning-and-preparation-work](planning-and-preparation-work/ "mention")

## Development / Integration

Once the project boundaries and overall planning/architecture work has been performed, the task of customizing SanteDB can commence.&#x20;

See: [Broken link](broken-reference "mention")

## Deployment

The deployment phase of SanteDB involves the installation, configuration, validation and testing of the environment.

See: [deployment](../installation-1/deployment/ "mention") for detailed information about deploying SanteDB software.

## Rollout

The rollout phase of SanteDB involves the actual onboarding of users and using the solution in an operational context.&#x20;

See: [rollout.md](../installation-1/rollout.md "mention") for more information about activities related to rollout of the SanteDB solution.
