# Configuring Identity Domains

The primary duty of a centralized MPI is to maintain records and identity of patients within a health enterprise (a hospital, province or state, country, etc.). It is very important that the MPI software have proper access controls and governance controls in place to control the issuing of new identifiers. For example:

* Your Immunization System shouldn't be the source of truth for LTC programme identifiers (correct issuing authority)
* You may not want to disclose mental health identifiers to a community outreach application (correct disclosure)
* You don't want facility associated identifiers being mistakenly assigned to patients  (correct usage)

{% hint style="info" %}
SanteDB provides built-in control of identity domains, however, as this topic is quite important to the functioning of an MPI relevant topics are reproduced here.
{% endhint %}

## Planning your Identity Domains

When planning a new identity domain (or identity domains when configuring your MPI) you'll need to ask the following questions:

* What is the scope of this identity? (to which objects does it apply)
* Which organization is the stewart / owner of the identity?
* What is the format of the identity domain?
* How does this identity relate to other identities in my jurisdiction?
* Is the identity unique? Or is it informative?

Once complete you'll need to gather information about each identity domain and design your configuration.

### OIDS , Namespace IDs, and URLs

SanteDB (and by extension SanteMPI) supports a variety of standards, each of which use different labels to identify an identity domain. For example, in FHIR an identity may appear as:

```markup
<identifier> 
    <use value="usual"/> 
    <type> 
      <coding> 
        <system value="http://terminology.hl7.org/CodeSystem/v2-0203"/> 
        <code value="MR"/> 
      </coding> 
    </type> 
    <system value="http://emrs.elbonia.elb/programme/hiv"/> 
    <value value="123457"/> 
  </identifier> 
```

Whereas that same identifier in an HL7v2 message would appear as:

```markup
123457^^^MOHS_EMR_HIV&&ISO^^P
```

Or in HL7v3 the identifier may appear as:

```markup
<id authority="1.2.3.4.5.6.7.8.9" value="123457" />
```

To properly ensure cross referencing between each of these interfaces, SanteDB will need to know the URL (used primarily in FHIR), the namespce ID (used primarily in HL7v2) and the OID/Universal ID (used primarily in HL7v3).

Since these all need to be unique, it is a good practice that your scheme for these values encompass the entity which owns the identifier, the programme area or department, and the system. For example, if the Ministry of Health runs an infectious disease programme in which an HIV EMR is used, a good Namespace ID for the MRN form that system may be: **MOH\_ID\_HIV\_EMR\_MRN**&#x20;

## Creating a New Identity Domain

To create a new identity domain (for example, a new programme identifier type), you'll use the [Reference Data](broken-reference) administration area and more specifically, the Identity Domain administration page within that administrative area. This will present you with a list of configured identity domains, you can click "CREATE" to create a new identity domain.

![](<../.gitbook/assets/image (37).png>)

### Configuring Core Properties

The first data collected by SanteDB when creating a new identity domain are the key identity domain properties including those discussed above as well as validation information for the identity domain.

![](<../.gitbook/assets/image (21).png>)

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

![](<../.gitbook/assets/image (116).png>)

#### Assigning App

In the example above, this new **MOH\_ID\_HIV\_EMR\_MRN** **** identity domain, only authenticated devices running the application org.santedb.disconnected\_client.android (the Android SanteDB Client) is the authoritative source of identifiers for this domain. Other systems can register patients and provide this identifier, however if the MPI doesn't recognize a new identity (say from OpenMRS) it will flag it as a DQ issue.

#### Scope

The scope dictates which types of objects can carry this type of identifier. Here the identifier can be assigned to any entity which is a Patient (a full registered patient in the MPI), a Person (a related person such as mother/father, or another person), and healthcare providers (this is just an example).

Whenever SanteMPI receives a registration that attempts to assign an identity in this domain to another type of entity (like a Place, Material, Immunization, etc.) it will be rejected.

#### Disclosure Policy

When specified, this parameter dictates the policy which must be granted to the principal which is accessing it, otherwise the identifier will be masked. For example, the set disclosure policy would require the user, device, and application to not have been prohibited access to the DISCLOSE HIV INFORMATION policy.&#x20;

If the user or remote system has not been explicitly granted that policy, it will be masked and the issuer of the request can establish an ELEVATED session with the MPI to gain access to the identifiers.
