# New ADO (nuado)

The persistence layer in SanteDB is largely a maintenance of the OpenIZ persistence layer which itself was originally written in 2009 for the MEDIC CR and MEDIC SHR. This data layer has over a decade of modifications, changes, etc. to it from a variety of authors during its lifetime.

This has lead to several performance issues with SanteDB, namely:

* The intended use of the OpenIZ persistence layer was for synchronization, so objects are deep-loaded in the persistence layer, regardless of whether the caller will use the information. There was no way for the caller to convey to the persistence layer that loading data is not needed.
* The persistence layer requires joining of non-versioned attributes to load data (i.e. versioned attributes and non-versioned attributes were stored as a master/detail view). This impacts query performance as the database needs to perform an extra join.
* There have been several technology enhancements to the .NET platform since the original design of the persistence layer which would optimize the manner in which database calls can be made.
* Missed properties via `.LoadProperty()` require duplicate hits to the database, regardless if the data persistence layer already made this query and determined there was no matching entries.

To fix this, a new persistence layer (on branch `feature/nuado` ) has been in development for several months. This new persistence layer:

* Performs lazy-loading of records from the database when the caller requests them (i.e. calling `Skip()`, `Take()`, `Count()`, etc. translates directly to SQL statements in the database rather than deep loading
* Allows the caller to use the `QueryPersistenceContext` to control the manner in which properties are loaded based on the caller's use case.
* Uses a pipeline architecture, where MDM, privacy, and other modifications to data are performed as a pipeline of steps rather than against pre-loaded enumerations.

{% hint style="info" %}
The refactoring of the entire SanteDB iCDR to the new ADO patterns is approximately 50% complete, and will be released as part of the 2.3.x series of SanteDB iCDR. The dCDR will follow refactoring to these new interfaces after the iCDR is stabilized.
{% endhint %}

## Query Result Set

The new persistence layer modifies all the data access classes to use the `IQueryResultSet<T>` interface. These interfaces support methods for skipping and taking records from the underlining data store in a method which reduces the data loaded from the SQL database.

The code below illustrates the modification of the SQL statement sent to the database by using the result set methods.

```
var dpe = ApplicationServiceContext.GetService<IRepositoryService<Patient>();

// Prepares the statement SELECT * FROM pat_tbl....
var patients = dpe.Find(o=>o.DateOfBirth <= DateTime.Now);

// Executes a SELECT EXISTS (....) rather than loading patients
if(patients.Any()) {

    // Modifies the statement above to SELECT * FROM pat_tbl OFFSET 10 ROW TAKE FIRST 10 ROWS ONLY
    patients = patients.Skip(10).Take(10);
    
    // Modifies statement above to SELECT COUNT(*) FROM (....)
    var patientCount = patients.Count();
}
```

Additionally, the application of any data modification processes (such as MDM or policy enforcement) is pipelined. This means that as records are read from the database, each record is operated on by the interested services.

### Result Set Implementations

| MemoryQueryResultSet    | Implementation of the `IQueryResultSet` which operates on an `IEnumerable` instance. This result set just passes any calls to the underlying enumerable object.                                                                                                                                          |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NestedQueryResultSet    | Implementation of the `IQueryResultSet` where a function is called for each retrieved object. This type of result set wrapper is useful when the yield function wishes to modify the result loaded from the wrapped result set.                                                                          |
| TransformQueryResultSet | Implementation of a `IQueryResultSet` which transforms a source record type to a destination record type using a transform function (`Func<TSource, TDestination>`) to map an object (in a pipelined manner) from A to B.                                                                                |
| MappedQueryResultSet    | A query result set which wraps an `IOrmResultSet` . When constructing this instance, the persistence layer should pass an instance of a `IMappedQueryProvider` which can be called by the ORM layer to skip/take/count and convert records from the data model layer to the business object model layer. |
| MappedStatefulResultSet | A specialized `MappedQueryResultSet` which operates on stateful query results from `IQueryPersistenceProvider`.                                                                                                                                                                                          |

&#x20;
