# Editing Demographic Information

To edit demographic information for a patient, click the pencil icon in the **Basic Information** panel.

![](<../../.gitbook/assets/image (90).png>)

This will switch the panel into editing mode.

![](<../../.gitbook/assets/image (6).png>)

### Editing Birth Details

The **Birth** tab contains details attached to the patient's demographic record related to their birth. The fields for this view are:

| Field       | Opt      | Purpose                                                                                                                                                                                                                                                                                       |
| ----------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DOB         | Required | The patient's date of birth. If **Approx** is checked, then the date of birth is assumed approximate (the year of birth representing the patient's age at point of registration)                                                                                                              |
| Gender      | Required | The patient's gender for the purposes of administration. This dropdown value is drawn from the AdministrativeGender concept set. Jurisdictions can modify this list based on their requirements and legislative environment related to gender.                                                |
| Birth Order | Optional | If the patient was born as part of a multiple birth (twins, triplets, etc.) this input allows you to indicate this, as well as select the birth order of the patient (if known). This can be used by your matching configuration to differentiate between twins with the same DOB, name, etc. |
| Birthplace  | Option   | Allows the selection of the facility, county, country, state, etc. where the patient was born.                                                                                                                                                                                                |

### Editing Names

SanteDB allows a single patient to have a multitude of names. The name input is found on the **Name** tab of the edit view, clicking this tab will enable the name editing functions.

![](<../../.gitbook/assets/image (121).png>)

{% hint style="info" %}
This input may appear with more or less inputs depending on the structure of names within your deployment.
{% endhint %}

The fields which may appear on this input include:

| Field     | Opt      | Purpose                                                                                                                                                                                                                                                                 |
| --------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name Type | Required | Allows the selection of the type of name being captured. This list is drawn from the **NameUse** concept set, and can be customized based on the needs of the jurisdiction.                                                                                             |
| Prefix    | Optional | The prefix of the name such as Mr., Mrs., Dr., Sir., etc.                                                                                                                                                                                                               |
| Given     | Required | The patient's given names (first name, middle names, initials, etc.). Depending on your configuration, this input may be tokenized when you press the space bar. This configuration can overcome scenarios where patients use their middle names in lieu of given name. |
| Family    | Required | The patient's family name(s). Depending on your configuration this input may be tokenized.                                                                                                                                                                              |
| Suffix    | Optional | The suffix for the name such as MD., Esq., etc.                                                                                                                                                                                                                         |

There are several common types of names which are built into SanteDB. Name types are controlled by changing the concept members of the NameUse concept set.

| Type            | Use                                                                                                                                                         |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bad Name        | Used to indicate that the patient used to be known by a particular name, however they no longer use this name.                                              |
| Search          | Indicates that the specific type of name is unknown, however it should be used for gathering search results.                                                |
| Anonymous       | A name which is used to anonymously receive treatment such as a fake name generated by a name generator to protect the sensitive nature of treatment.       |
| Ideographic     | Indicates the name is constructed of ideograms. This type of name should be used if using Kanji or other ideographic representation of a name.              |
| Phonetic        | Indicates the name is constructed using a phonetic alphabet such as katakana, hiragana, Burmese script, etc.                                                |
| Alphabetic      | Indicates the name is a romanization of a phonetic or ideographic name. In Japanese this would equate to romaji script.                                     |
| Religious       | The name used for religious purposes, such a Friar John or Pastor Jim.                                                                                      |
| Artist          | The name is a pseudonym/alias for artistic purposes.                                                                                                        |
| Pseudonym       | The name is a pseudonym that the patient is known as (this represent AKA)                                                                                   |
| Indigenous      | A name assigned by a tribe or for use in tribal practices.                                                                                                  |
| Maiden Name     | A name the patient had prior to marriage.                                                                                                                   |
| License         | The patient's name as it appears on an official license. This can be used for physicians who practice under a name different than their legal name.         |
| Official Record | The patient's "official" name within the master patient index or SanteDB instance.                                                                          |
| Legal           | The patient's "legal" name as they use for interacting with government services. This may be the name as it appears on a birth certificate, passport, etc.  |

### Editing Addresses

SanteDB allows a single patient to have multiple addresses each with a different purpose. Accessing the address entry is done clicking on the **Address** tab.

![](<../../.gitbook/assets/image (57).png>)

This input area can change based on the configuration of your instance of SanteMPI. There are three types of address entry generally provided:

* Fully Structured - You will be presented with a single drop-down which will allow you to select a single address entry from a pre-populated list of "official" addresses.
* Semi-Structured (Shown Above) - You will be presented with a  complex address entry whereby you can select a few structured fields (usually state/province, county and city) and enter freetext for the remainder of the address.
* Freeform - You will be presented with freetext inputs where you can manually enter each field.

{% hint style="info" %}
The labels of the fields in the address entry screen can also be customized based on your configuration of SanteMPI. For example, County/District may appear in your interface as **Township **.
{% endhint %}

The type of addresses which can be captured in SanteDB/SanteMPI are listed below, this list can be customized by editing the concept set AddressUse.

| Type                    | Use                                                                                                                                                                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Birth                   | The address where the patient was born. This concept is deprecated use "RESIDENCE AT BIRTH" instead.                                                                                                                                    |
| Country of Origin       | The address of the patient's origin, this can including an address of a migrant worker back in their home country.                                                                                                                      |
| Residence At Birth      | The address of the patient at birth. This may be a home village, or parental address.                                                                                                                                                   |
| Birth Delivery Location | The address where the patient was born. This can be a hospital address, home address where a home birth was performed. Etc.                                                                                                             |
| Temporary               | A temporary address where the patient is known to be residing. This can be used for tourists, those of no fixed address, etc.                                                                                                           |
| Postal Address          | An address where correspondence can be sent/routed. This can be a P.O. Box or delivery pickup location.                                                                                                                                 |
| Physical Visit          | An address where a clinician can physically visit the patient.                                                                                                                                                                          |
| Bad Address             | An address that is no longer valid.                                                                                                                                                                                                     |
| Public                  | An address which is publicly known, for example, if the patient's address appears on a public record this type would be selected.                                                                                                       |
| Workplace               | The patient's primary workplace address.                                                                                                                                                                                                |
| Vacation Home           | The patient's vacation home such as a cottage, recreational vehicle park, etc.                                                                                                                                                          |
| Primary Home            | The patient's primary home address. Use this type of address if the patient only has one address, or in the case where a patient lives in multiple homes (such as joint custody of minor) the home where the patient primarily resides. |
| Home Address            | Subsequent home addresses for the patient.                                                                                                                                                                                              |
| Phonetic                | The address is a local address represented in a phonetic script such as katakana, hiragana, Burmese script, etc.                                                                                                                        |
| Ideographic             | The address as represented in an ideographic form such as kanji.                                                                                                                                                                        |
| Alphabetic              | The address as represented in a Romanized representation of an original script. For example, romaji.                                                                                                                                    |

### Editing Contact Addresses

You can edit the patient's primary methods of contact using the **Contact** tab. The contact tab presents a list of address types and allows for the specification of whether the contact address is an electronic address (e-mail) or telephone address.

![](<../../.gitbook/assets/image (115).png>)

Based on your configuration of SanteDB the list of available contact types may be different. The list of address types can be changes by editing the TelecommunicationsAddressUse concept set.

The types of addresses are:

| Type              | Use                                                                                                                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Answering Service | A telephone or e-mail address which routes to a mailbox rather than direct line to the patient.                                            |
| Emergency         | A telephone or e-mail address to be contacted in cases of emergency.                                                                       |
| Mobile            | A telephone number which can receive SMS and MMS information.                                                                              |
| Pager             | A telephone number which can only receive short pager messages or can only buzz the user (i.e. a beeper)                                   |
| Home/Public       | The primary home phone number or e-mail address to be used for general communications.                                                     |
| Temporary         | A temporary telephone or e-mail address which the patient may use during registration however may not be in service for subsequent visits. |
| Work              | A work telephone number or e-mail address                                                                                                  |

### Editing Death Details

When a patient dies, or is reported as deceased the demographic record can be updated to reflect this. To report a patient as deceased use the **Death** tab.

![](<../../.gitbook/assets/image (58).png>)

Here the patient has been indicated as deceased sometime around May 5, 2020. It is also possible to record the place of death of the patient.

{% hint style="info" %}
The death details on the patient's demographic record is merely to mark the patient as deceased. SanteDB supports more robust death reporting such as **Cause of Death** , **Suspected Death**, and links to procedures/conditions which are suspected to have caused the death. These, however are stored as Acts in SanteDB's CDR.
{% endhint %}

### Editing Extra Associations

SanteDB 2.0.10 introduces a new editing tab for **Extra** information. This information allows the editing of extended relationship types between the patient and other entities such as organizations, countries, etc.

![](<../../.gitbook/assets/image (92).png>)

The relationship types are listed below for additional assistance:

| Relationship     | Multi? | Description                                                                                                                                     |
| ---------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Caregiver(s)     | Yes    | One or more organizations or providers which are dedicated caregivers for the patient. (For example: CHW, at-home nurse, nursing home contact). |
| Citizenship(s)   | Yes    | One or more countries for which the patient is a citizen.                                                                                       |
| Coverage/Sponsor | Yes    | The organization that provides insurance coverage for the patient or is sponsoring the patient's care.                                          |
| Primary Facility | No     | The dedicated facility where this patient receives care.                                                                                        |
| Employer         | Yes    | One or more organizations where the patient is known to work.                                                                                   |
| Primary Provider | Yes    | The patient's primary care provider (family doctor) or other known providers.                                                                   |
| School           | Yes    | One or more educational institutions where the patient is attending school.                                                                     |
