# Act Relationships

Often time acts are related to one another via the ActRelationship entity. Act relationships are important, as typically acts cannot be standalone. For example, one cannot simply “Observe” something without having an encounter. An example of several types of interactions within SanteDB are described below:

1.  **Patient Presents to receive an Immunization:**\
    &#x20;In this use case the primary act is a PatientEncounter whereby participants include the clinician performing the vaccination (performer), the patient (record target), the clinic (service delivery location). The patient may be weighed prior to receiving the immunization that represents a component act of type Observation, and the administration of the vaccine represents a substance administration with relations to one or materials administered&#x20;

    <img src="../../../../.gitbook/assets/image (104).png" alt="" data-size="original">
2.  **Scheduling a second dose of an antigen:**\
    &#x20;In this use case the primary act is a PatientEncounter with mood of Intent (i.e. I intend to have an encounter) and date in the future. The PatientEncounter may have one or more substance administrations with mood of Intent that represent the vaccinations that are intended to be given at the appointment. &#x20;

    <img src="../../../../.gitbook/assets/image (128).png" alt="" data-size="original">
3.  **Patient Presents for Appointment:** In this use case, the patient presents for the scheduled appointment. The encounter fulfills the appointment request.  \


    <img src="../../../../.gitbook/assets/image (114).png" alt="" data-size="original">
4. **Forecasted vaccination:**\
   &#x20;In this use case a decision support system identifies a patient which needs to receive a vaccine. The forecasting engine may create a PatientEncounter with mood of Proposed that indicates that a computer system is proposing an action to occur. When the patient presents for their vaccination the clinician creates a new PatientEncounter with mood of Event that fulfills the PatientEncounter with mood of Proposed (i.e. the clinician is saying “I am acting on your proposal”).
