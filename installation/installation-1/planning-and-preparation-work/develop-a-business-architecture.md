# Develop a Business Architecture

SanteDB, SanteIMS and SanteMPI are interoperable software solutions for managing clinical data. While a software solution is a means to implement business use cases, it is not the end in itself. Typically the software implements or realizes business processes.&#x20;

It is important, therefore, to develop a business architecture which describes the human and organizational architecture. This includes:

* Documenting new business processes to be used in clinic among the various connected systems.
* Document data capture standards, and agreement between organizations on the format and use of each data element (establish a common understanding of data elements from a business use).
* Formalize inter-departmental or inter-organization processes for sharing, accessing, and disclosing data stored in the common SanteDB infrastructure.&#x20;

{% hint style="info" %}
Implementers of SanteDB, SanteMPI or SanteIMS are encouraged to follow practices established by their own project management office (PMO) and local country patterns. This article serves as general guidance to the contents/structure of the business level architecture.
{% endhint %}



## Developing User Journeys

User stories are a great tool for describing how users interact with each system and how each system interacts with each other. User journeys may be documented using BPMN activity diagrams or using a user journey map.

Regardless of the format, the user journey should:

* Identify the major steps of the business process being performed.
* Identify the goals of the user and the system (what is the user and/or system trying to accomplish?)&#x20;
* Identify the humans involved (or organizations, departments, ministries, etc.)
* Identify the systems involved&#x20;
* Illustrate how the humans interact with the systems, and how humans and systems interact with one another.&#x20;

For example, consider the user journey to issue a new national health identifier to patient for Demoland.&#x20;

![](<../../../.gitbook/assets/image (183).png>)

