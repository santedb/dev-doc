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

### Community Technology Preview Versions

Starting with SanteDB 2.x, versions are differentiated between a technology preview version and a hardened/LTS version using the minor build number. Minor builds which are even numbered are considered stable and no API changes are permitted (2.0.x, 2.2.x, 2.4.x, etc.). Builds with odd numbered minor versions are considered technology preview builds (2.1.x, 2.3.x, 2.5.x). CTP releases are suitable for use for developers, pilots, etc. and each revision within the minor build should be relatively compatible with one another.

CTP releases may, however, contain new features or enhancements which have not been deployed by the SanteDB team in a production context. These releases typically follow on another. For example, the 2.1.x CTP releases are used as the basis for the 2.2.x stable releases.&#x20;

As an example, the New ADO refactor represents a major re-write of the database access layer. When this layer is ready for CTP rollout they will fill the 2.3.x release series. Once the SanteDB team confirms the new versions for performance and stability in a production context (in at least one country) the minor of 2.3.x will be released as 2.4.x , at which time no changes are permitted to the APIs.

##

