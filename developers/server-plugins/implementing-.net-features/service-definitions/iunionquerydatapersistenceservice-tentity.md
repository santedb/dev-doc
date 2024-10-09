`IUnionQueryDataPersistenceService&lt;TEntity>` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a data persistence provider that can store and continue queries

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Union|IEnumerable&lt;TEntity>|*Expression`1[]* **queries**<br/>*Guid* **queryId**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalCount**<br/>*IPrincipal* **overrideAuthContext**<br/>*ModelSort`1[]* **orderBy**|Queries or continues a query|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyUnionQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IUnionQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IUnionQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query
	/// </summary>
	public IEnumerable<TEntity> Union(Expression`1[] queries,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalCount,IPrincipal overrideAuthContext,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IUnionQueryDataPersistenceService&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IUnionQueryDataPersistenceService_1.htm)
