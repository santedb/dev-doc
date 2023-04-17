# Identity Domain Management

Identity domains must be registered in the SanteDB iCDR before they can be used in messaging applications. For more information about the planning and purpose of identity domains consult [configuring-identity-domains.md](../../../../installation/installation-1/planning-and-preparation-work/develop-an-information-architecture/configuring-identity-domains.md "mention")

## Identity Domain List

When opening the Reference Data page for Identity Domains, administrators will be presented with a listing of all active identity domains configured on the iCDR or dCDR instance.

![](<../../../../.gitbook/assets/image (444) (1) (1) (1).png>)

The controls for this table are shared with other administrative panel functions (edit, delete, un-delete, etc.).

## Creating a New Identity Domain

To create a new identity domain (for example, a new programme identifier type), you'll use the [Reference Data](broken-reference) administration area and more specifically, the Identity Domain administration page within that administrative area. This will present you with a list of configured identity domains, you can click "CREATE" to create a new identity domain.

![](<../../../../.gitbook/assets/image (37).png>)

### Configuring Core Properties

The first data collected by SanteDB when creating a new identity domain are the key identity domain properties including those discussed above as well as validation information for the identity domain.

![](<../../../../.gitbook/assets/image (21) (1).png>)

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

### Authority and Scope

The authority and scope configuration area will dictate how SanteDB discloses the specified identifier, which system(s) can assign the identifier, and the scope (objects which can be assigned the identifier).

![](<../../../../.gitbook/assets/image (116).png>)

#### Assigning App

In the example above, this new **MOH\_ID\_HIV\_EMR\_MRN**  identity domain, only authenticated devices running the application org.santedb.disconnected\_client.android (the Android SanteDB Client) is the authoritative source of identifiers for this domain. Other systems can register patients and provide this identifier, however if the MPI doesn't recognize a new identity (say from OpenMRS) it will flag it as a DQ issue.

#### Scope

The scope dictates which types of objects can carry this type of identifier. Here the identifier can be assigned to any entity which is a Patient (a full registered patient in the MPI), a Person (a related person such as mother/father, or another person), and healthcare providers (this is just an example).

Whenever SanteMPI receives a registration that attempts to assign an identity in this domain to another type of entity (like a Place, Material, Immunization, etc.) it will be rejected.

#### Disclosure Policy

When specified, this parameter dictates the policy which must be granted to the principal which is accessing it, otherwise the identifier will be masked. For example, the set disclosure policy would require the user, device, and application to not have been prohibited access to the DISCLOSE HIV INFORMATION policy.&#x20;

If the user or remote system has not been explicitly granted that policy, it will be masked and the issuer of the request can establish an ELEVATED session with the MPI to gain access to the identifiers.
