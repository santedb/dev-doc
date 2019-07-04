# Acts

Acts in the SanteDB data model represent actions taken by entities to other entities. In this lens, we can say that an act represents everything that “happens” to entities. This mechanism of storage allows the SanteDB data model to adapt to different jurisdictions with relative ease.

There are five different types of acts that are supported by the default SanteDB schema \(Figure 1\).

![Figure 1 - Act Classes](../../../.gitbook/assets/image%20%2823%29.png)

* **Patient Encounters:** Represent an act whereby a patient presents, or is intended to present for care.
* **Observations:** Represent an act whereby an entity observes something. Observations can include codified observations such as diagnoses, textual values such as a free-text description of an event, or a quantity such as weight or heart rate.
* **Substance Administrations:** A substance administration is representing an act whereby a substance, such as a vaccine is administered to a patient.
* **Order:** An order is a special type of stock act and represents a request by an entity to transfer stock from one place to another.
* **Procedures:** A procedure is a type of act in which the physical state of the record target or target entity is changed.
* **Financial Transaction:** Which is used whenever a financial transaction, or an exchange of financial goods occurs.

### Class Concepts

Acts are classified into one of these four types based upon their ClassConcept code. This dictates what type of Act the particular tuple in the database represents. 

| Act Class | Code | Description |
| :--- | :--- | :--- |
| Observation | OBS | Indicates that the act represents a value which was observed. |
| Substance Administration | SBADM | Indicates that the act represents the administration of a substance to an entity. |
| Patient Encounter | ENC | The act represents an encounter between one or more providers of care and one or more clients of care. |
| Registration | REG | The act represents a registration whereby new data was collected about an entity. |
| Account Management | ACCM | The act represents the management \(adjustment\) of an account. |
| Supply | SPLY | The act represents the supply of one or more materials to/from one or more entities. |
| Condition | COND | The act represents a chronic or recurring problem or health condition. |
| Procedure | PROC | The act represents a clinical procedure which was performed on the client of care. |
| Battery | BAT | The act represents a series of procedures, observations, administrations, etc.  |
| Transport | TRANS | The act represents the physical transporting of materials to/from one or more entities. |
| Account | ACCT | The act represents an active account \(financial, stock, etc.\) on which transactions can be performed. |
| Financial Transaction | FTRANS | The act represents a financial transaction where monies are exchanged between one or more entities. |
| Invoice Element | INVE | The act represents a sub-element of a financial transaction. |

The class concept list is extensible.

### Mood Concepts

Additionally, Acts are classified by Mood via the MoodConceptId. The mood of an act identifies the mood or method of operation of the act, moods include:

| Mood | Code | Description |
| :--- | :--- | :--- |
| Proposal | PRPS | Indicates that the act was proposed by a system process such as a business rule, or clinical protocol. |
| Intent | INT | Indicates that a human intends to perform the act in the future, however the act has not yet occurred. |
| Event | EVN | Indicates that the act has actually occurred, or is occurring. |
| Request | RQO | Indicates that a person is requesting that the act occur. It is used to support order workflows.  |
| Promise | PRMS | Indicates that the act represents the promise to fulfill a request. |

### Relationships

Often time acts are related to one another via the ActRelationship entity. Act relationships are important, as typically acts cannot be standalone. For example, one cannot simply “Observe” something without having an encounter. An example of several types of interactions within SanteDB are described below:

1. **Patient Presents to receive an Immunization:**  
    In this use case the primary act is a PatientEncounter whereby participants include the clinician performing the vaccination \(performer\), the patient \(record target\), the clinic \(service delivery location\). The patient may be weighed prior to receiving the immunization that represents a component act of type Observation, and the administration of the vaccine represents a substance administration with relations to one or materials administered 

   ![](../../../.gitbook/assets/image%20%2817%29.png)

2. **Scheduling a second dose of an antigen:**  
    In this use case the primary act is a PatientEncounter with mood of Intent \(i.e. I intend to have an encounter\) and date in the future. The PatientEncounter may have one or more substance administrations with mood of Intent that represent the vaccinations that are intended to be given at the appointment.  

   ![](../../../.gitbook/assets/image%20%2825%29.png)

3. **Patient Presents for Appointment:**  In this use case, the patient presents for the scheduled appointment. The encounter fulfills the appointment request.    


   ![](../../../.gitbook/assets/image%20%2821%29.png)

4. **Forecasted vaccination:**  In this use case a decision support system identifies a patient which needs to receive a vaccine. The forecasting engine may create a PatientEncounter with mood of Proposed that indicates that a computer system is proposing an action to occur. When the patient presents for their vaccination the clinician creates a new PatientEncounter with mood of Event that fulfills the PatientEncounter with mood of Proposed \(i.e. the clinician is saying “I am acting on your proposal”\).

### States

SanteDB Act support attribution of the current status of an act using the state machine illustrated in Figure 2. 

![Figure 2 - Act States](../../../.gitbook/assets/image%20%284%29.png)

The states of an act are:

* **New :** Indicates that the act has yet to be reviewed and//or that business processing rules have yet to be executed.
* **Active :** Indicates that an act is currently occurring or being actioned. This state is used, for example, if an encounter is still occurring however has not completed.
* **Complete :** Indicates that the act has occurred. If the act is of a mood code such as intent, request, etc, the _complete_ status indicates that the request or intent is complete and has been fulfilled.
* **Nullified :** Indicates that the act was created in error, and never occurred.
* **Obsolete :** Indicates that the act did occur, however the information is no longer accurate, or has been amended.

