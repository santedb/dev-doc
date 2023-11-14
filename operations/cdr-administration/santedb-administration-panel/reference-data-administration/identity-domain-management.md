# Identity Domain Management

Identity domains must be registered in the SanteDB iCDR before they can be used in messaging applications. For more information about the planning and purpose of identity domains consult [configuring-identity-domains.md](../../../../installation/installation-1/planning-and-preparation-work/develop-an-information-architecture/configuring-identity-domains.md "mention")

## Identity Domain List

When opening the Reference Data page for Identity Domains, administrators will be presented with a listing of all active identity domains configured on the iCDR or dCDR instance.

![](<../../../../.gitbook/assets/image (538).png>)

The controls for this table are shared with other administrative panel functions (edit, delete, un-delete, etc.).

## Creating a New Identity Domain

To create a new identity domain (for example, a new programme identifier type), you'll use the [Reference Data](broken-reference) administration area and more specifically, the Identity Domain administration page within that administrative area. This will present you with a list of configured identity domains, you can click "CREATE" to create a new identity domain.

![](<../../../../.gitbook/assets/image (724).png>)

### Configuring Core Properties

The first data collected by SanteDB when creating a new identity domain are the key identity domain properties including those discussed above as well as validation information for the identity domain.

![](<../../../../.gitbook/assets/image (19).png>)

The core properties are:

| Field            | Description                                                                                                                                                                               | Example                                                                                                                                         |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Namespace ID     | The namespace used in the CX.4.1 of HL7 messages.                                                                                                                                         | MOH Infectious Disease HIV EMR programme MRN                                                                                                    |
| Universal ID     | The universal OID which identifies the identity domain.                                                                                                                                   | This is an IANA PEN for Fyfe Software Inc. projects for illustrative purposes. You can also use 2.25.XXXX where XXXX is a UUID in decimal form. |
| URL              | The unique URL of the identity domain.                                                                                                                                                    | An example of the Elbonia MOH HIV Programme EMR                                                                                                 |
| Name             | A human readable name for the identity domain.                                                                                                                                            |                                                                                                                                                 |
| Validation Regex | A regular expression that validates identifiers the MPI receives. Note that the MPI may not reject messages, but rather may use the Data Quality extensions to flag invalid identifiers.  | 10 digit decimal                                                                                                                                |
| Unique           | When unique, an identifiers is treated as reliable in the matching process. Also, only the assigner may assign new identities and duplicates will be flagged as an error.                 |                                                                                                                                                 |

{% hint style="info" %}
If there are more than one administrator be sure to use the search function first to ensure you're not configuring a duplicate identifier.
{% endhint %}

### Validation

The validation section of the identity domain screen allows administrators to specify how identifiers in the domain are subjected to the [DataQualityValidation](../../../../user-guides-and-training/santempi/the-patient-dashboard/data-quality-tab.md) when objects are registered. These also control the input controls for identifier information in the user interface.

<figure><img src="../../../../.gitbook/assets/image (788).png" alt=""><figcaption></figcaption></figure>

#### Validation Regex

The validation regex is used to validate the format of the identifier. This is how the identifier appears when presented on cards, and what is expected to be submitted to the CDR. As the validation regex is entered, an example of an identifier in the format provided will be provided. Some simple regular expressions are included below for the reader's convenience, and can be combined as necessary.

| Regular Expression | Validates                            | Example |
| ------------------ | ------------------------------------ | ------- |
| `[A-Z]{1,3}`       | 1-3 upper-case letters               | ABC     |
| `\d{5}`            | Exactly 5 digits (0-9)               | 029382  |
| \[MF]              | Only M or F                          | M       |
| \[A-Za-z]{6}       | Exactly 6 upper or lower-case letter | AJFHDJS |
| \\-                | A -                                  |         |

#### Check Digit Type

If the identifier has a check digit scheme which does not appear in the identifier number itself (or if you would like a check digit generated when the UI stores the data) you can supply an independent checkdigit algorithm.

#### Custom Format Validator

The custom format validator is used to validate identifiers using special implementation logic. Custom validators can be used to validate generated identifiers (using information in the submitted Patient for example), or can be used to validate inline check-digit algorithms (i.e. if the check digit is the last 2 digits of the identifier value).

### Authority and Scope

The authority and scope configuration area will dictate how SanteDB discloses the specified identifier, which system(s) can assign the identifier, and the scope (objects which can be assigned the identifier).

![](<../../../../.gitbook/assets/image (762).png>)

#### Scope

The scope dictates which types of objects can carry this type of identifier. Here the identifier can be assigned to any entity which is a Patient (a full registered patient in the MPI), a Person (a related person such as mother/father, or another person), and healthcare providers (this is just an example).

Whenever SanteMPI receives a registration that attempts to assign an identity in this domain to another type of entity (like a Place, Material, Immunization, etc.) it will be rejected.

#### Disclosure Policy

When specified, this parameter dictates the policy which must be granted to the principal which is accessing it, otherwise the identifier will be masked. For example, the set disclosure policy would require the user, device, and application to not have been prohibited access to the DISCLOSE HIV INFORMATION policy.&#x20;

If the user or remote system has not been explicitly granted that policy, it will be masked and the issuer of the request can establish an ELEVATED session with the MPI to gain access to the identifiers.

### Assigning Authority

{% hint style="info" %}
This section describes a feature that is only in SanteDB v3.0&#x20;
{% endhint %}

The assigning authority of the identity domain allows an administrator to prohibit the issuance of new authoritative identifiers, save for the list of designated applications provided.&#x20;

<figure><img src="../../../../.gitbook/assets/image (789).png" alt=""><figcaption></figcaption></figure>

The application is assigned by selecting the [security application credential ](../../santedb-icdr-admin-console/application-administration.md)which is permitted to issue identifiers in the domain. The administrator may also specify whether submissions from the indicated source are authoritative or informative.
