# Configuring Privacy Controls

{% hint style="info" %}
This article documents and uses features of SanteDB 3.0. The implementation of these features on previous versions of SanteDB may be partial and/or missing.&#x20;
{% endhint %}

All SanteDB solutions (SanteMPI, SanteEMR, and SanteIMS) are designed to support adherence to a variety of privacy controls which can be used by implementers to conform to local privacy legislation such as:

* [The Canadian Personal Information Protection and Electronic Documents Act ](https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-personal-information-protection-and-electronic-documents-act-pipeda/r\_o\_p/)(PIPEDA)&#x20;
* [General Data Protection Regulation](https://gdpr.eu/) (GDPR)

Because SanteDB provides a platform for implementation of many different use cases in many different legislative environments, it is the responsibility of implementers to properly configure the necessary controls in the SanteDB product to match their use case. This article provides brief guidance on how such configurations are made to the underlying privacy control system using legislatively agnostic terminology.

## Accountability

When deploying SanteDB and its related software, be sure to appoint a member on your team (or establish a team) which is accountable for assessing the compliance of your SanteDB implementation with the local privacy legislation. Specifically:

* Develop and Document Personal Information Policies and Practices
* Develop a Privacy Management Programme/Procedures
* Complete a [Privacy Impact Assessment](../planning-and-preparation-work/developing-privacy-impact-assessments.md) and identify:
  * What information is required to be collected?&#x20;
  * How is the information to be collected?
  * What is the information used for?
  * How is the information secured?
  * Which users have access to the information?
  * What third parties is the information shared with?
  * What are the policies/timelines for retaining and disposing of the information?
* Develop and document procedures for:
  * Informing Patients, Providers and other stakeholders of the use of their personal data.
  * Obtaining informed consent of the individuals whose data is used and stored in SanteDB
  * Ensuring that information collected is current and up to date.
  * Investigating breaches, fielding requests for investigations, inquiries requests for obtaining access to private information (from authorities, patients, etc.)
  * Training employees and staff members on the privacy procedures and policies being implemented.

All of these assets should be made publicly available to patients, providers and staff members who will interact with your deployment of SanteDB.

## Identify Purpose, Limiting Collection, Disclosure and Retention of Data

SanteDB is a generic CDR which can store an almost infinite number of data fields related to Patients, Providers, Locations, Staff Members, etc. However, not all of this data is used for every context. For example, using SanteIMS as an EIR will have different uses and needs for collecting data than SanteMPI as a national patient index.&#x20;

Implementing a limitation on the collection of data in SanteDB begins with reviewing the data requirements of your project and reviewing the [SanteDB Conceptual Information Architecture](../../../santedb/data-and-information-architecture/conceptual-data-model/). After determining the necessary fields, you should decide:

* Do we need to collect this information for internal use? (for example, matching or notifications)
* If we collect this data, what do we need to do to safeguard it? (for example, encrypting it or restricting disclosure)
* If we collect this data, how long does it remain active?

### Limiting Data Collection

For information in the conceptual information model which will not be used, the SanteDB configuration needs to be updated to restrict the use of the fields in question. This is done by editing the `santedb.config.xml` file on the iCDR server using either the [Configuration Tool](../../../operations/server-administration/configuration-tool/), or editing the file directly.&#x20;

The `App Settings` is used to change the behavior of data which is collected. These settings will:

* Reject any message which contains the restricted data fields listed regardless of where/how the data originated into the CDR (FHIR, HL7, etc.)
* Hide any inputs on the user interface which are used to collect this information

The `Action` column describes what this setting does when set to TRUE in the configuration:

* `Forbid` -> The data field is permitted and stored by default, when the setting is enabled, the information is forbidden:
  * Requests to register or update the data result in a rejection of the message
  * User interface elements to collect the data disappear
* `Allow` -> The data field is forbidden by default, when the setting is enabled, the information is allowed:
  * Requests to register or update the data will not result in a rejection message
  * User interface elements to collect the data will appear.

<table><thead><tr><th>Setting</th><th width="355">Data Field</th><th>Action</th></tr></thead><tbody><tr><td><code>forbid.patient.name.family</code></td><td>Patient Family Names</td><td>Forbid</td></tr><tr><td><code>forbid.patient.name.given</code></td><td>Patient Given Names</td><td>Forbid</td></tr><tr><td><code>forbid.patient.name.prefix</code></td><td>Patient Name Prefixes (Mr, Mrs, etc.)</td><td>Forbid</td></tr><tr><td><code>forbid.patient.name.suffix</code></td><td>Patient Name Suffixies (Jr, Sr, etc.)</td><td>Forbid</td></tr><tr><td><code>forbid.patient.address.state</code></td><td>Patient Addresses with State information</td><td>Forbid</td></tr><tr><td><code>forbid.patient.address.county</code></td><td>Patient Addresses with County information</td><td>Forbid</td></tr><tr><td><code>forbid.patient.address.city</code></td><td>Patient Addresses with City information</td><td>Forbid</td></tr><tr><td><code>forbid.patient.address.precinct</code></td><td>Patient Addresses with Precinct information</td><td>Forbid</td></tr><tr><td><code>forbid.patient.address.street</code></td><td>Patient Addresses with Street information</td><td>Forbid</td></tr><tr><td><code>forbid.patient.address.postalcode</code></td><td>Patient Addresses with PostalCode information</td><td>Forbid</td></tr><tr><td><code>allow.patient.religion</code></td><td>Patient Religious Affiliation</td><td>Allow</td></tr><tr><td><code>allow.patient.ethnicity</code></td><td>Patient Ethnic Group</td><td>Allow</td></tr><tr><td><code>allow.patient.livingArrangement</code></td><td>Patient Living Arrangement (Alone, Ward of State, Orphan, etc.)</td><td>Allow</td></tr><tr><td><code>allow.patient.maritalStatus</code></td><td>Patient Marital Status (Single, Married, Divorced, etc.)</td><td>Allow</td></tr><tr><td><code>allow.patient.educationLevel</code></td><td>Patient Education Level</td><td>Allow</td></tr><tr><td><code>forbid.person.occupation</code></td><td>Patient, Provider, or Relative's Occupation</td><td>Forbid</td></tr><tr><td><code>forbid.person.gender</code></td><td>Patient, Provider or Relative's Administrative Gender </td><td>Forbid</td></tr><tr><td><code>forbid.person.vipStatus</code></td><td>Patient, Provider or Relative's VIP status</td><td>Forbid</td></tr><tr><td><code>forbid.person.nationality</code></td><td>Patient, Provider or Relatives Nationality</td><td>Forbid</td></tr></tbody></table>

#### Propagation to dCDR Instances

The settings listed above can be propagated to dCDR instances by populating the `<publicSettings>` element in the `AmiConfigurationSection`:

```xml
<section xsi:type="AmiConfigurationSection">
    <welcomeMessage>Welcome to SanteMPI</welcomeMessage>
    <publicSettings>    
      <add key="allow.patient.maritalStatus" value="true" />
```

This can also be set using the Configuration Tool by navigating to `Messaging > Administrative Management Interface`

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### In Configuration Tool

To configure these settings in the configuration tool, navigate to the `Settings Editor` tab and select `ApplicationServiceContextConfigurationSection` and expand `App Settings`.

<figure><img src="../../../.gitbook/assets/image (524).png" alt=""><figcaption></figcaption></figure>

Then, enter each setting as a new entry and set the value to `true` or `false` as illustrated.

<figure><img src="../../../.gitbook/assets/image (525).png" alt=""><figcaption></figcaption></figure>

#### Configuration File

The information can be updated in the configuration file in the `<section xsi:type="ApplicationServiceContextConfigurationSeciton">` element:

```xml
<section xsi:type="ApplicationServiceContextConfigurationSection" 
    allowUnsignedAssemblies="true" threadPoolSize="4">
  <serviceProviders>
    <!-- Service Provider Lines -->
  </serviceProviders>
  <appSettings>
    <add key="allow.patient.martialStatus" value="true" />
    <add key="allow.patient.ethnicity" value="false" />
    <add key="allow.patient.educationLevel" value="true" />
    <add key="allow.patient.livingArrangement" value="true" />
    <add key="allow.patient.religion" value="true" />
  </appSettings>
</section>
```

### Limiting Concept Sets

Another method of limiting the data collection is the restriction of individual codified fields. For example, a deployment may wish to allow the collection of a person's occupation (the default setting, or `forbid.person.occupation=false`) but restrict the collection to two categories used for eligibility determination. To do this, the [Concept Set Editor ](../../../operations/cdr-administration/santedb-administration-panel/concept-dictionary-administration/)can be used to edit the members of the concept set to only those required in the deployment. The concept set bindings for the data fields above are as follows:

| Field                         | Concept Set                 |
| ----------------------------- | --------------------------- |
| Patient Marital Status        | `MaritalStatus`             |
| Patient Religious Affiliation | `Religion`                  |
| Patient Living Arrangement    | `LivingArrangement`         |
| Patient Education Level       | `EducationLevel`            |
| Patient Ethnicity             | `Ethnicity`                 |
| Person Occupation             | `OccupationType`            |
| Person Administrative Gender  | `AdministrativeGenderCode`  |
| Person VIP Status             | `VeryImportantPersonStatus` |

### Limiting Data Disclosure

As documented in the [SanteDB Privacy Architecture](../../../santedb/privacy-architecture.md) article, SanteDB can limit the disclosure of data from the CDR to clients who lack the appropriate policies. Configuring this privacy guard involves the following steps:

* Create policies using the [Administration Console's Policy ](../../../operations/server-administration/santedb-icdr-admin-console/policy-administration.md)editor or the [Administration Panel's Policy Manager](../../../operations/cdr-administration/santedb-administration-panel/security-administration/managing-policies.md) which represent the disclosure policies.
* Create a business rule [which tags relevant data](../../../santempi/recipes/adding-security-policy-based-on-occupation.md) with your applet which tags data matching the desired conditions under which the policy should be applied. Examples are:
  * Tag SubstanceAdministrations with `HIV Care Only` policy when the `Product` administered is an ARV
  * Tag Patients with `VIP Care Only` policy when the `Occupation` indicates the patient is a Government Official
* Configure the iCDR with the appropriate data policy actions using the [Configuration Tool Data Privacy Filtering](../../../operations/server-administration/configuration-tool/security-settings/data-privacy-filtering.md) option.
* Ensure that the [Data Privacy Filter](../../../developers/server-plugins/implementing-.net-features/service-definitions/data-privacy-enforcement-provider.md) service is enabled.

#### Auditing Data Disclosure

Administrators are encouraged to ensure that the Audit and Accountability subsystem of their iCDR and dCDR are appropriate configured for their use case. This is done via the Configuration Tool in the `Audit and Accountability` section.

<figure><img src="../../../.gitbook/assets/image (527).png" alt=""><figcaption></figcaption></figure>

Administrators should ensure that the appropriate data actions are being persisted and/or (if required) shipped to a central audit repository for review by privacy officers.

<figure><img src="../../../.gitbook/assets/image (528).png" alt=""><figcaption></figcaption></figure>

Once configured, privacy officers can use the SanteDB administration panel to review these audits.

{% content-ref url="../../../operations/cdr-administration/santedb-administration-panel/security-administration/reviewing-audits.md" %}
[reviewing-audits.md](../../../operations/cdr-administration/santedb-administration-panel/security-administration/reviewing-audits.md)
{% endcontent-ref %}

### Limiting Data Retention

Limitation of the retention of data (including audits, and any CDR clinical data) is handled by the [Data Archiving Service](../../../developers/server-plugins/implementing-.net-features/service-definitions/data-archiving-service.md) and ensuring that the [Data Retention Job](http://santesuite.org/assets/doc/net/html/T\_SanteDB\_Core\_Jobs\_DataRetentionJob.htm) is enabled and scheduled. Generally, this process involves:

* Determine the appropriate retention parameters which are required such as cutoff dates for archiving or purging the data, lookups, etc.
* Determine the types of data to which the retention policies apply (Patients, Observations, etc.) and configuring the appropriate retention strategies.&#x20;
* Enabling the retention job and setting the schedule for retention.

These settings are documented in the configuration tool's Data Retention Service Configuration.

## Safeguarding Personal Information

SanteDB provides a variety of methods for securing personal information while it is being transmitted to third parties, and while it is stored on the file system. There are several articles which explain the configuration of these options:

{% content-ref url="securing-santedb-configuration.md" %}
[securing-santedb-configuration.md](securing-santedb-configuration.md)
{% endcontent-ref %}

{% content-ref url="securing-santedb-databases.md" %}
[securing-santedb-databases.md](securing-santedb-databases.md)
{% endcontent-ref %}

{% content-ref url="securing-the-apis.md" %}
[securing-the-apis.md](securing-the-apis.md)
{% endcontent-ref %}

These safeguards should be enabled prior to the deployment and operationalization of your SanteDB deployment to ensure that your local legislative requirements are adhered to.

## Ensuring Data Accuracy

Decisions and information which are made on out of date, or inaccurate data can adversely impact patient safety, as well as the protection of their data. It is therefore important that appropriate procedures are put in place to ensure that data is accurate and conflicting/old data is not actioned upon.&#x20;

The following non-technical procedures should be considered when operationalizing your SanteDB software:

* Ensure that staff members and providers are trained to regularly update Patient profile information at the start of each visit.
* Ensure that patient's are authenticated using some of reliable method (government issued photo ID, storing a photograph of the patient, biometric extensions, etc.)
* Ensure that staff, and business rules are configured to review the data quality/detected issues prior to making decisions (see: [Data Quality](../../../operations/server-administration/host-configuration-file/data-quality-services.md) Services)

SanteDB provides a limited function for tagging and/or rejecting data which is incomplete or does not adhere to certain data quality markers.&#x20;

{% content-ref url="../../../operations/server-administration/host-configuration-file/data-quality-services.md" %}
[data-quality-services.md](../../../operations/server-administration/host-configuration-file/data-quality-services.md)
{% endcontent-ref %}

{% content-ref url="../../../user-guides-and-training/santempi/the-patient-dashboard/data-quality-tab.md" %}
[data-quality-tab.md](../../../user-guides-and-training/santempi/the-patient-dashboard/data-quality-tab.md)
{% endcontent-ref %}

{% content-ref url="../../../operations/cdr-administration/santedb-administration-panel/cdr-administration/data-quality-rules.md" %}
[data-quality-rules.md](../../../operations/cdr-administration/santedb-administration-panel/cdr-administration/data-quality-rules.md)
{% endcontent-ref %}

## Individual Access

It is important that individuals (Patients, Providers, etc.) can challenge a data custodian to enumerate the data which the CDR holds about them, and to understand who has observed and/or interacted with this information. In SanteDB this is addressed via:

* Exporting the Patient's CDR data in discrete RIM format, which can be performed using the HDSI query APIs (see: [Health Data Service Interface](../../../developers/service-apis/health-data-service-interface-hdsi.md)) and/or developing and providing a summary report for end-users (see: [Business Intelligence Services - Report](../../../developers/extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/bi-asset-definitions/))
* Enabling SanteGuard and reviewing the [Audit & Access Trail](../../../user-guides-and-training/santeguard.md#audit-and-access-trail-tab) tab on the patient's profile.&#x20;

SanteDB does not provide a direct method of purging data from within the user interface directly. Administrators can configure data retention rules which archive and subsequently purge data based on tags they configure in their own deployment applets.
