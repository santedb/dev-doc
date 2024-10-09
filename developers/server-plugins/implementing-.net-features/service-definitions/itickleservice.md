`ITickleService` in assembly SanteDB.Client version 3.0.1980.0

# Summary
Represents a service which provides tickles for the user (popup messages)

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|DismissTickle|void|*Guid* **tickleId**|Dismiss a tickle|
|SendTickle|void|*Tickle* **tickle**|Send a tickle to the user screen|
|GetTickles|IEnumerable&lt;Tickle>|*Expression&lt;Func&lt;Tickle,Boolean>>* **filter**|Get tickles|

# Implementations


## InMemoryTickleService - (SanteDB.Client)
An implementation of the [ITickleService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Tickles_ITickleService.htm) which uses memory structures 
            to temporarily hold tickles for the user interface

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Tickles.InMemoryTickleService, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Client.Tickles;
/// Other usings here
public class MyTickleService : SanteDB.Client.Tickles.ITickleService { 
	public String ServiceName => "My own ITickleService service";
	/// <summary>
	/// Dismiss a tickle
	/// </summary>
	public void DismissTickle(Guid tickleId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Send a tickle to the user screen
	/// </summary>
	public void SendTickle(Tickle tickle){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get tickles
	/// </summary>
	public IEnumerable<Tickle> GetTickles(Expression<Func<Tickle,Boolean>> filter){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ITickleService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Tickles_ITickleService.htm)
* [InMemoryTickleService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Tickles_InMemoryTickleService.htm)
