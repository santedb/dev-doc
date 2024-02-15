# Concepts

The `Concepts` page in the SanteDB administration panel allows data administrators to manage the core concepts which are registered in SanteDB. Concepts are used as a canonical form of structured terminology internally within SanteDB's CDR.&#x20;

For example, when registering a patient and setting the gender to "Male" the database record carries the canonical concept of "Male" (uuid: `f4e3a6bb-612e-46b2-9f77-ff844d971198`) . This UUID is consistent for all males between all installations of SanteDB permitting data portability. This concept would then be mapped to a wire-level reference term:

* `M` if the patient is being expressed in HL7v2
* `male` if the patient is being expressed via FHIR

This architecture isolates the SanteDB CDR from changes in wire-formats.

{% hint style="info" %}
Users should familiarize themselves with SanteDB's [concept dictionary architecture ](../../../../santedb/data-and-information-architecture/conceptual-data-model/concept-dictionary/)prior to administering the concept dictionary.
{% endhint %}

The concept dictionary installed in your copy of SanteDB is displayed when the concept page is opened.

<figure><img src="../../../../.gitbook/assets/image (495).png" alt=""><figcaption></figcaption></figure>

## Creating Concepts

Creating a new concept is done via the `Create` button on the concept summary page.&#x20;

<figure><img src="../../../../.gitbook/assets/image (503).png" alt=""><figcaption></figcaption></figure>

Each concept has the following components:

* `Mnemonic` - A globally unique human readable label for the concept. This mnemonic is used by programmers and humans to reference the mnemonic using a more friendly name than the UUID
* `Classification` - Used for internal model validation, the classification lets the CDR understand the overall categorization under which the concept falls.
* `Name(s)` - Human readable descriptions of the concept which appear in SanteDB's user interface.
* `Set Membership` - Groupings of concepts within a concept set.
* `Reference Terms` - Wire level manifestations of the concept in a particular code system.

After creating the concept the administrator will be taken to the edit concept page.

## Viewing/Editing Concepts

Administrators can change concepts that have been registered in the SanteDB concept dictionary by clicking the View option.

<figure><img src="../../../../.gitbook/assets/image (509).png" alt=""><figcaption></figcaption></figure>

The `Concept Properties` panel allows for the editing of the core properties of the concept including the removal of concept set memberships, names, and the mnemonic.

<figure><img src="../../../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
Editing the `Mnemonic` of the concept is not recommended if the concept has been used in a user interface or referenced programmatically (in reports, business rules, etc.). Editing the `Mnemonic` should only occur to correct typo's and errors immediately after creation.
{% endhint %}

## Reference Term Management

The user interface on the concept editing screen only permits the removal of a concept from a reference term. To add an association to a reference term, edit the Reference Terminology directly in the [Code Systems ](code-systems.md)management screen.

<figure><img src="../../../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure>

## Concept Status

The status of the concept can be set by clicking the state button in the concept header. This action will prohibit use of the concept in user interfaces, while maintaining referential integrity with existing data in the database and allowing data integrations to continue to use the concept.

<figure><img src="../../../../.gitbook/assets/image (520).png" alt=""><figcaption></figcaption></figure>

