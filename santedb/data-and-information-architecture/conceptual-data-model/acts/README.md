# Acts

Acts in the SanteDB data model represent actions taken by entities to other entities. In this lens, we can say that an act represents everything that “happens” to entities. This mechanism of storage allows the SanteDB data model to adapt to different jurisdictions with relative ease.

There are five different types of acts that are supported by the default SanteDB schema (Figure 1).

![Figure 1 - Act Classes](<../../../../.gitbook/assets/image (166).png>)

* **Patient Encounters:** Represent an act whereby a patient presents, or is intended to present for care.
* **Observations:** Represent an act whereby an entity observes something. Observations can include codified observations such as diagnoses, textual values such as a free-text description of an event, or a quantity such as weight or heart rate.
* **Substance Administrations:** A substance administration is representing an act whereby a substance, such as a vaccine is administered to a patient.
* **Order:** An order is a special type of stock act and represents a request by an entity to transfer stock from one place to another.
* **Procedures:** A procedure is a type of act in which the physical state of the record target or target entity is changed.
* **Financial Transaction:** Which is used whenever a financial transaction, or an exchange of financial goods occurs.
