# SanteDB Versioning

SanteDB releases have two versions associated with them:

* Semantic Version -> Which is used for determining compatibility of assemblies within the SanteDB solutions, dependencies, etc.
* Informational Version -> Which is used to describe the overall release.

## Versioning Information (1.x and 2.x)

### Semantic Versions

The semantic versions of SanteDB look similar to this:

```
[major].[minor].[revision].[build]
```

Where:

* **Major:** Describes the major release.&#x20;
  * _**Even**_ numbered major versions are release versions
  * _**Odd**_ numbered major versions are development versions between releases
* **Minor:** Describes the overall patch level within the particular version of SanteDB
* **Revision:** Is used to describe patch level. These are usually random (but increasing) values.

### Legacy Versions (1.x)

SanteDB originally was implemented as a revision of the core OpenIZ backend. This was implemented on .NET Framework 4.5.2, Xamarin and PCL Profile7 assemblies. These versions begin with the major revision 1.x , ending 1.128.0 (Iqaluit).

Since PCL has been deprecated for some time, a refactor of the code to .NET Standard 2.0 was recently performed.

### .NET Standard Versions (2.x)

Starting with SanteDB named version Jasper , the entire shared assembly infrastructure has been ported to .NET Standard 2.0. Since these assemblies are incompatible with the PCL infrastructure and .NET 4.5.2,  the entire project was upgraded to .NET 4.7 and the major version rev'd to 2.x series.&#x20;

{% hint style="info" %}
We're still in the process of updating our documentation to reflect this change of underlying frameworks.
{% endhint %}

### Version 3.0&#x20;

SanteDB version 3.0 and its related solutions (SanteMPI 3.0, SanteIMS 3.0, SanteEMR 3.0) have many enhancements which improve the efficiency and maintainability of SanteDB products. These features are documented in detail throughout the wiki and tagged with:

{% hint style="info" %}
This Page Documents a feature in SanteDB v3.0
{% endhint %}

In summary the enhancements are:

* Refactoring of the entire data persistence layer to use more efficient database calls (see: [new-ado-nuado.md](../../santedb/software-architecture/new-ado-nuado.md "mention"))
* Implementation of the data mart and data warehouse which allows for secondary use of SanteDB data outside of the RIM and allows implementers to specify their own data marts (see: [data-marts.md](../../developers/applets/business-intelligence-bi-assets/bi-asset-definitions/data-marts.md "mention"))
* Ability to customize the data quality rules within the administrative user interface (see: [data-quality-rules.md](../../operations/cdr-administration/santedb-administration-panel/cdr-administration/data-quality-rules.md "mention"))
* Ability to import data directly from CSV files into the CDR using the administrative interface (see: [importing-data.md](../../operations/cdr-administration/santedb-administration-panel/cdr-administration/importing-data.md "mention"))
* Ability to register new publish/subscribe targets in the administrative user interface, and more granular control of the dispatcher queues for subscriptions (see: [pub-sub-manager.md](../../operations/cdr-administration/santedb-administration-panel/system-administration/pub-sub-manager.md "mention"))
* Improvements to the iCDR / dCDR onboarding routine and ability to map data signature and authentication certificates to users, applications, and devices (see: [#certificate-mapping](../../operations/cdr-administration/santedb-administration-panel/security-administration/managing-devices.md#certificate-mapping "mention"))
* Full ability to manage the Concept Dictionary via the administrative interface, including ability to import concept sets and reference terminology from CSV files directly from file system (see: [concept-dictionary-administration](../../operations/cdr-administration/santedb-administration-panel/concept-dictionary-administration/ "mention"))
* Completely refactored Clinical Decision Support (CDSS) system which allows for editing of CDSS definitions directly in the user interface in realtime (including realtime debugging of CDSS rules) (see: [decision-support-library](../../operations/cdr-administration/santedb-administration-panel/cdr-administration/decision-support-library/ "mention"))
* New text based CDSS asset type which allows for easy creation and modification of CDSS rules (rather than XML format) (see: [cdss-definitions.md](../../developers/applets/cdss-protocols/cdss-definitions.md "mention"))
* CDSS as a service operations allow for third party callers to invoke CDSS rules over the REST interfaces
* Care Pathways allowing for enrolment and storage of clinical care plans based on a logical grouping of care patterns (see: [care-pathways.md](../../user-guides-and-training/santeemr/emr-administration/care-pathways.md "mention"))
* Improvements to the reporting infrastructure to support new, complex types of graphing and report layouts
* Ability to export most CDR configuration and metadata to dataset files from the user interface (when the `Export CDR Metadata` policy is enabled)
*

