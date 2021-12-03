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

###

##

