# Code Systems

The code system management index is where administrators will manage the global list of code systems in SanteDB. A [Code System](../../../../santedb/data-and-information-architecture/conceptual-data-model/concept-dictionary/#reference-terms) is a collection of reference terms defined by a standards body and is typically used on the SanteDB [FHIR](../../../../operations-1/standard-operating-procedures/hl7-fhir/), [HL7v2](../../../../developers/service-apis/hl7v2.md), or GS1 interfaces.

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Code systems can be viewed, deleted, or created using the relevant buttons in the user interface.

## Creating Code Systems

The process of creating a new code system commences with the **Create** button on the code system list.&#x20;

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Fields for this user interface are:

* **Name:** A short, descriptive, human readable name for the code system.
* **Domain:** A unique (within the context of the current SanteDB instance) short name for the code system. In HL7v2, this is the CX.4 portion of the code, for example: `CODE^^^DOMAIN`. It is also the short name that appears within internal SanteDB HDSI view model payloads.
* **OID:** A universally unique identifier for the code system. This is used in HL7v2 in the CX.4.3 portion of a code such as `CODE^^^&2.25.XXXXXX&ISO` and in HL7v3/CDA based transactions. This should be one of:
  * An IANA Private Enterprise Number based OID
  * An HL7 Registered OID
  * A UUID expressed as `2.25.XXXXXXX`
* **URL**: The url is a unique resource locator to the definition of the terminology. This is typically used on HL7 FHIR interfaces.
* **Version**: The version of the terminology being imported or expressed by the code system.
* **Description**: A long-form description of the code system

Once the administrator has completed the necessary fields, the **Save** button may be used to create the code system.

## Editing Code Systems

Existing code systems can be edited by selecting **Edit** from the code system list. This will present a code system dashboard.

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### Core Properties

The core properties of the code system captured in the creation step of the code system can be modified by selecting **Edit** on the panel and changing the relevant properties.

### Adding Reference Terms

To add a reference term, the **Add** option can be used above the reference term list.

<figure><img src="../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

The mnemonic (or wire code) is entered into the reference term creation dialog, this needs to be unique within the scope of the code system. Additionally, one or more names can be added to the reference term. These should be the official translation of the code as they are expected to appear in HL7 messages.

Additionally, one or more internal concepts in the SanteDB concept dictionary need to be mapped to the reference term. The administrator should select the nature of the mapping as:

* SAME\_AS: The reference term has an identical semantic meaning as the concept in SanteDB
* INVERSE\_OF: The reference term has the opposite meaning as the concept in SanteDB
* NEGATION\_OF: The reference term indicates a negation of the concept in SanteDB (for example: a code indicating a negative diagnosis)
* NARROWER\_THAN: The refernece term has a meaning that is narrower in meaning to the concept in SanteDB
* WIDER\_THAN: The reference term has a meaning that is more broad in meaning to the concept in SanteDB

iThe administrator should then search for a concept in the SanteDB database to be mapped. Alternatively, selecting the Magic Wand button will allow the user to create a brand new concept (with the same names as entered on the reference term).

<figure><img src="../../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
It is **highly recommended** that users do not use the wire-level reference term mnemonic as the mnemonic for the concept being created. SanteDB concept mnemonics are like labels or variable names, and should be globally unique within the SanteDB instance and should be descriptive in their nature.
{% endhint %}

After the necessary information is entered into the creation dialog, clicking **Add** will complete the necessary opterations to associate the concept with the reference term. Additionally, users may use the **Add and Create Another** option to enter multiple codes.

<figure><img src="../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

### Importing Code System Terms

For larger terminologies with thousands of codes, it may be easier to adapt a flat file such as Excel spread sheet of the terms to a comma-separated-value (CSV) file with columns:

* `Mnemonic` - Contianing the wire level code
* `Name` - Containing the official translation in the desired language
* `Concept` (optional) - Containing the Mnemonic of an existing (or new) concept to be created
* `Mapping` (optional) - Containing the nature of the mapping between `Concept` and `Mnemonic` (`SameAs`,`NarrowerThan`, etc.)

<figure><img src="../../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

This file can be uploaded into the reference term dialog, and uploaded.
