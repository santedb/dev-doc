`IAliasProvider` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Provider for name and place aliasing

## Description
Some implementations of the SanteDB engine allow for searching of data based on aliases. This aliasing
            allows SanteDB to map an inbound query parameter like 'Bob' to 'Robert' or 'Will' to 'Bill' and 'William'.
            The service is responsible for providing the known aliases for each name into the SanteDB infrastructure, and
            these can be accessed using the HDSI extended query filter: 
```
name.component.value=:(alias|Bob)&gt;=1.0
```
  
            which indicates that the aliases of the stored name should match Bob.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetAlias|IEnumerable&lt;ComponentAlias>|*String* **name**|Gets the known alias names and score for the alias|
|AddAlias|void|*String* **name**<br/>*String* **alias**<br/>*Double* **weight**|Add an alias to the alias provider|
|RemoveAlias|void|*String* **name**<br/>*String* **alias**|Remove the specified alias|
|GetAllAliases|IDictionary&lt;String,IEnumerable&lt;ComponentAlias>>|*String* **filter**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**|Get all aliases|

# Implementations


## AdoNameAliasService - (SanteMPI.Persistence.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteMPI.Persistence.ADO.Services.AdoNameAliasService, SanteMPI.Persistence.ADO, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAliasProvider : SanteDB.Core.Services.IAliasProvider { 
	public String ServiceName => "My own IAliasProvider service";
	/// <summary>
	/// Gets the known alias names and score for the alias
	/// </summary>
	public IEnumerable<ComponentAlias> GetAlias(String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add an alias to the alias provider
	/// </summary>
	public void AddAlias(String name,String alias,Double weight){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove the specified alias
	/// </summary>
	public void RemoveAlias(String name,String alias){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all aliases
	/// </summary>
	public IDictionary<String,IEnumerable<ComponentAlias>> GetAllAliases(String filter,Int32 offset,Nullable<Int32> count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IAliasProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAliasProvider.htm)
* [AdoNameAliasService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteMPI_Persistence_ADO_Services_AdoNameAliasService.htm)
