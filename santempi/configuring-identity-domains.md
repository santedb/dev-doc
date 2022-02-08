# Planning Identity Domains and Assigning Authority

The primary duty of a centralized CDR is to maintain records from various sources of information. Identity of that information (patient identity, place identity, event identity, etc.) within a health enterprise (a hospital, province or state, country, etc.) is of paramount importance.&#x20;

Furthermore, the governing of those identities should also be considered. For example:

* Your Immunization System shouldn't be the source of truth for LTC programme identifiers (correct issuing authority)
* You may not want to disclose mental health identifiers to a community outreach application (correct disclosure)
* You don't want facility associated identifiers being mistakenly assigned to patients  (correct usage)

{% hint style="info" %}
SanteDB provides built-in control of identity domains, however, as this topic is quite important to the functioning of an MPI relevant topics are reproduced here.
{% endhint %}

## Planning your Identity Domains

When planning a new identity domain (or identity domains when configuring your MPI) you'll need to ask the following questions:

* What is the scope of this identity? (to which objects does it apply)
* Which organization is the steward / owner of the identity?
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

##
