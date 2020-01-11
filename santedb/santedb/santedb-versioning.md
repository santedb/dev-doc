# SanteDB Versioning

SanteDB releases have two versions associated with them:

* Semantic Version -&gt; Which is used for determining compatibility of assemblies within the SanteDB solutions, dependencies, etc.
* Informational Version -&gt; Which is used to describe the overall release.

### Semantic Versions

The semantic versions of SanteDB look similar to this:

```text
[major].[minor].[revision].[build]
```

Where:

* **Major:** Describes the major release. 
  * _**Even**_ numbered major versions are release versions
  * _**Odd**_  numbered major versions are development versions between releases
* **Minor:** Describes the overall patch level within the particular version of SanteDB
* **Revision:** Is used to describe patch level. These are usually random \(but increasing\) values.

### Informational Versions

Informational versions are usually tied to milestones or date ranges. Typically an informational version may be comprised of one or more assemblies with different semantic versions. Informational version names are mostly for humans. The informational version names are alphabetical \(with Algonquin being the first and Iqaluit being the most recent\) 

* Algonquin - 0.x series
* Bluenose - 0.9.x series
* Chippewa - 0.9.2.x series
* Dalhousie - 0.9.4.x series
* Edmonton - 0.9.7.x series
* Fredericton - 1.0.0 series
* Gananoque - 1.10 - 1.50 
* Halifax - 1.50 - 1.99
* Iqaluit - 1.100 - 1.119 \(Current\)
* Jasper - 1.120 - 139
* Kamloops - 1.140 - 1.159

