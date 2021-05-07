# Version 3.x Roadmap

SanteDB 1.x was a near direct refactor of the original OpenIZ core, which had components from the MEDIC Service Core project dating back to 2008/2009. While SanteDB 2.x was a refactor off this .NET Framework and PCL code to .NET Standard, there are still many components and patterns \(ghosts\) of the original service core code from 2008. 

The SanteDB Version 3.x roadmap seeks to fully remove these patterns and re-implement many of the core services. However, this presents a problem in that it makes incremental change difficult, and will break the services. For this reason, much of the Version 3.x roadmap is currently in the design / wishlist phase.

## Refactor I/O Calls to TAP Pattern

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

## Refactor Persistence Layer

{% hint style="info" %}
The persistence layer refactor is currently underway and the code for these features can be found at: [https://github.com/santedb/santedb-server/tree/feature/nuado](https://github.com/santedb/santedb-server/tree/feature/nuado)
{% endhint %}

The persistence layer is quite messy, and sub-optimal. It was written \(as mentioned\) starting in 2009 and has over a decade of modifications, changes, etc. to it. A major refactor of the persistence layer could be performed as part of a v2.5 version which cleans the implementation up. The goals of this work item would be:

* Refactor all current persistence classes to use yield returns so on-demand mapping and loading of data is performed.
* Refactor process of loading, so that only direct properties are loaded either:
  * At the persistence layer, do not load any associated properties and rely on callers calling : patient.LoadProperty\(o=&gt;o.Names\) , which is sub-optimal since it requires establishing a new connection rather than loading on an existing connection \(this point may be moot\)
  * At the persistence layer, only load direct associated properties that are commonly used directly. Refactor the current LoadState property to an internal value which allows the persistence layer to indicate a value was loaded and needn't be re-checked.
* Refactor and clean up the query writer in OrmLite to use only LINQ mapping and expression tree mapping, rather than converting to/from the HTTP representation.
  * This would require a complete rewrite of the IQueryHack interfaces which currently allow for the optimization by manually creating SQL. Such an IQueryHack would need to be changed to accept an Expression&lt;T&gt; with the desired filters.

## Add Complex Guard Expressions

Currently within SanteDB, simple guard classifications can be done on a classifier property, for example:

```text
Patient?telecom[WorkPlace].value=john@johnstuff.com
```

However, there is a need to support more complex guard expressions wherein a full HDSI guard expression can be placed into the query builder. For example:

```text
Patient?telecom[type.mnemonic=EMAIL&use.mnemonic=WorkPlace].value=john@johnstuff.com
```

The requirements of this nested guard are:

* The builder should be able to express simple guards \(the current format\) as the current LINQ translation of `Telecoms.Where(guard=>guard.UseConcept.Mnemonic == WorkPlace).Any()` 
* The builder should be able to process the complex guards \(the new format\) as a similar LINQ expression of: `Telecoms.Where(guard=>guard.TypeConcept.Mnemonic == "EMAIL" && guard.UseConcept.Mnemonic == "WorkPlace").Any(v=>v.Value == "john@johnstuff.com")` 
* The persistence layer and SQL translators will also need to be updated to support this type of expression

