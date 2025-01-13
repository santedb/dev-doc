# Visit Types & Flows

{% hint style="info" %}
This page documents a feature in SanteDB 3.0 with the SanteEMR 3.0 plugins installed and enabled on the administrative portal.
{% endhint %}

Whenever a patient is checked-in for a visit in SanteEMR, the visit classification (the `typeConcept` ) is used to determine the flow of that patient through the visit lifecycle. This allows for the patient to be returned or held in different waiting areas depending on the status of the visit.&#x20;

SanteEMR's state flows are linked to encounter types using the **Visit Types & Flows** administrative screen on the **SanteEMR** area of the administrative panel.&#x20;

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## Creating/Editing a Visit Type

Creating and editing a visit type are the similar processes. When creating a visit type, users will enter the classification concept and will identify the workflow states that are applicable to this type of visit. For example, creating an inpatient visit type and flow may appear as:

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

In this flow, the administrator has indicated that the visit flow for an inpatient visit in their deployment is as follows:

* Patients are Checked-In first
* Patient may be assigned to a ward or may be placed in a waiting state before being placed on the ward
* After care is done the state of the encounter is awaiting for discharge

## Defining New States & Flows Between States

The states for the EMR flows are contained in the **Concept Dictionary** in the **EMREncounterTags** concept set. The administrator may create new states by creating new concepts in this concept set.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Each state is then assigned one or more concept relationships of type **State Flow** to indicate the outward flow of a state to another. This is administered on the concept detail screen.

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
