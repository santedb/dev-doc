# Documenting Identifiers

The primary duty of a centralized CDR (and more specifically an MPI) is to maintain records from various sources of information. Identity of that information (patient identity, place identity, event identity, etc.) within a health enterprise (a hospital, province or state, country, etc.) is of paramount importance.&#x20;

Furthermore, the governing of those identities should also be considered. For example:

* Your Immunization System shouldn't be the source of truth for LTC programme identifiers (correct issuing authority)
* You may not want to disclose mental health identifiers to a community outreach application (correct disclosure)
* You don't want facility associated identifiers being mistakenly assigned to patients  (correct usage)

{% hint style="info" %}
SanteDB provides built-in control of identity domains, however, as this topic is quite important to the functioning of an MPI relevant topics are reproduced here.
{% endhint %}

## Surveying Identifiers

It is important in any SanteDB deployment (especially for SanteMPI) to perform a survey of identifiers which are used in the context in which the solution will be deployed.&#x20;

Implementers should note:

* The types of medical and non-medical identifiers which are currently in use.
* Which organizations are responsible for the maintenance and issuing of the identifier.
* The lifecycle of the identifier (i.e. how is a new identifier issued, are the holders authenticated, etc.)
* The format and requirements of the identifier (are there check digits, if so what are they?)
* The use of the identifier (billing, identification, tagging, etc.)
* The scope of the identifier (what type of objects carry this identifier? Patients, vials, boxes etc.)
* Commonality of the identifier
  * What proportion of the population carries this identifier?&#x20;
  * Is it normal for the identifier to be readily available?
  * Is it culturally acceptable (or legally acceptable) to use this identifier? (for example: disclosure of Social Security Number to a pharmacist)

## Planning Identity Domains

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

## Resources

An identity domain worksheet has been created and shared below. This worksheet contains instructions and example data which should assist implementers in the organization of their identity domain planning work.

{% file src="../.gitbook/assets/SanteMPI Identity Domain Worksheet.xlsx" %}

To use the spreadsheet:

1. Enumerate the issuing organizations in the implementation context (organizations, ministries, etc.) and complete the **Issuing Authority** sheet.
2. Enumerate each of the identification domains which are used in the context to which SanteDB or SanteMPI will be deployed.
3. Update the cover sheet of your worksheet with relevant metadata about the sheet.
