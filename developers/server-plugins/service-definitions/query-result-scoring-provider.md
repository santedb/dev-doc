`IQueryScoringService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a service that can score queries

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Score|IEnumerable&lt;IQueryResultScore&lt;T>>|*Expression&lt;Func&lt;T,Boolean>>* **filter**<br/>*IEnumerable&lt;T>* **results**|Requests that the matching operation score the specified series of results|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyQueryScoringService : SanteDB.Core.Services.IQueryScoringService { 
	public String ServiceName => "My own IQueryScoringService service";
	/// <summary>
	/// Requests that the matching operation score the specified series of results
	/// </summary>
	public IEnumerable<IQueryResultScore<T>> Score<T>(Expression<Func<T,Boolean>> filter,IEnumerable<T> results){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IQueryScoringService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IQueryScoringService.htm)
