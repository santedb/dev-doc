# SanteDB Versioning

SanteDB releases have two versions associated with them:

* Semantic Version -&gt; Which is used for determining compatibility of assemblies within the SanteDB solutions, dependencies, etc.
* Informational Version -&gt; Which is used to describe the overall release.

## Versioning Information \(1.x and 2.x\)

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

### Legacy Versions \(1.x\)

SanteDB originally was implemented as a revision of the core OpenIZ backend. This was implemented on .NET Framework 4.5.2, Xamarin and PCL Profile7 assemblies. These versions begin with the major revision 1.x , ending 1.128.0 \(Iqaluit\).

Since PCL has been deprecated for some time, a refactor of the code to .NET Standard 2.0 was recently performed.

### .NET Standard Versions \(2.x\)

Starting with SanteDB named version Jasper , the entire shared assembly infrastructure has been ported to .NET Standard 2.0. Since these assemblies are incompatible with the PCL infrastructure and .NET 4.5.2,  the entire project was upgraded to .NET 4.7 and the major version rev'd to 2.x series. 

{% hint style="info" %}
We're still in the process of updating our documentation to reflect this change of underlying frameworks.
{% endhint %}

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
* Iqaluit - 1.100 - 1.119 
* Jasper - 2.0.0 - 2.0.9 
  * Upgrade to .NET Standard and .NET Framework 4.8
* Kelowna - 2.0.10 - 2.0.29
* Langley - 2.0.30 - 2.0.49
* Montreal - 2.0.50 - 2.0.069
* Nanaimo - 2.0.70 - 2.0.89
* Ontario - 2.0.90 - 2.0.109
* Pickering - 2.0.110 - 2.0.129

## Version 3.x Roadmap

SanteDB 1.x was a near direct refactor of the original OpenIZ core, which had components from the MEDIC Service Core project dating back to 2008/2009. While SanteDB 2.x was a refactor off this .NET Framework and PCL code to .NET Standard, there are still many components and patterns \(ghosts\) of the original service core code from 2008. 

The SanteDB Version 3.x roadmap seeks to fully remove these patterns and re-implement many of the core services. However, this presents a problem in that it makes incremental change difficult, and will break the services. For this reason, much of the Version 3.x roadmap is currently in the design / wishlist phase.

### Refactor I/O Calls to TAP Pattern

Currently all I/O calls, from the REST layer, to the data access layer are using legacy .NET patterns. This work items seeks to correct this by refactoring all I/O calls to the Task Async Pattern. This will require a complete refactoring of the following core components:

#### RestSrvr

The lightweight REST API I/O calls will need to be refactored to support async/await service implementations. Some work has been done to experiment with this in the v2.x core. The changes made to this layer would not be breaking as the RestSrvr layer is the entry point to much of the iCDR and dCDR core functions.

Notes from the experimentation:

* The OperationDispatcher should detect if the bound behavior returns a Task or Task&lt;T&gt; and executes the operation as an await\(ed\) call.
* The OperationDispatcher detected if any of the parameters of the operation were a CancellationToken, and if so, it would pass the cancellation token form the WinHTTP API to the method to indicate a cancel down the call chain.
* The actual binding implementation should be added \(similar to NancyFX\) to allow for piggy-backing on either the WinHTTP , Mono HTTP  \(used by the dCDR on RPi, Docker, and Android\) or Kestrel server \(for web-hosting only\). Currently the RestSrvr only uses the HttpServer implementation which does not pass the CancellationToken

#### Repository and DataPersistence Services

The entire Repository and DataPersistence service layer would need to be refactored such that they return IAsyncEnumerable&lt;T&gt;. The notes for this feature are:

* All I/O calls for insert, save, etc. should return Task&lt;T&gt; and allow the passing of a CancellationToken to allow for cancellation of I/O operations.
* Query calls \(such as Find and Query\) should return IAsyncEnumerable&lt;T&gt; to permit async streams of data from the underlying layer.
  * The query calls should also be refactored to use yield returns minimizing the computational resources required to process results from the database.
  * The interface should also permit callers to indicate whether a count of total results is required, or whether simple fuzzy paging \(i.e. "there is another page"\) should be called

Unfortunately this refactor will change the service calls such that any existing code and plugins would break. There are two options the team has discussed:

* Create IAsyncX versions of each of the service interfaces \(not ideal\)
  * This would mean the creation of an IAsyncDataPersistenceService&lt;T&gt; interface which contains only async versions of the call
  * This would allow existing plugins to operate, however would add burden to maintenance as each implementer must implement both the regular service provider and the IAsyncX version.
* Add Async methods to the existing service definitions
  * This would add allow existing plugins to continue to operate as normal, however would require any implementations of the existing services to be refactored to add async methods.
  * This has the same maintenance issues as the IAsyncX method

### Refactor Persistence Layer

The persistence layer is quite messy, and sub-optimal. It was written \(as mentioned\) starting in 2009 and has over a decade of modifications, changes, etc. to it. A major refactor of the persistence layer could be performed as part of a v2.5 version which cleans the implementation up. The goals of this work item would be:

* Refactor all current persistence classes to use yield returns so on-demand mapping and loading of data is performed.
* Refactor process of loading, so that only direct properties are loaded either:
  * At the persistence layer, do not load any associated properties and rely on callers calling : patient.LoadProperty\(o=&gt;o.Names\) , which is sub-optimal since it requires establishing a new connection rather than loading on an existing connection \(this point may be moot\)
  * At the persistence layer, only load direct associated properties that are commonly used directly. Refactor the current LoadState property to an internal value which allows the persistence layer to indicate a value was loaded and needn't be re-checked.
* Refactor and clean up the query writer in OrmLite to use only LINQ mapping and expression tree mapping, rather than converting to/from the HTTP representation.
  * This would require a complete rewrite of the IQueryHack interfaces which currently allow for the optimization by manually creating SQL. Such an IQueryHack would need to be changed to accept an Expression&lt;T&gt; with the desired filters.

