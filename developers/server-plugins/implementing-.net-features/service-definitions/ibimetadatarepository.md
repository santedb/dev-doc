`IBiMetadataRepository` in assembly SanteDB.BI version 3.0.1980.0

# Summary
Represents a metadata repository for the BIS services

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|IsLocal|Boolean|R|True if the source of metadata is local|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Query|IEnumerable&lt;TBisDefinition>|*Expression&lt;Func&lt;TBisDefinition,Boolean>>* **filter**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**|Query metadata repository for|
|Query|IQueryResultSet&lt;TBisDefinition>|*Expression&lt;Func&lt;TBisDefinition,Boolean>>* **filter**|Query metadata repository for|
|Get|TBisDefinition|*String* **id**|Get the specified BI definition by identifier|
|Remove|void|*String* **id**|Removes the specified BI definition from the repository|
|Insert|TBisDefinition|*TBisDefinition* **metadata**|Inserts the specified BI definition into the repository|

# Implementations


## AppletBiRepository - (SanteDB.BI)
Represents a default implementation of a BIS metadata repository which loads definitions from loaded applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.AppletBiRepository, SanteDB.BI, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoBiRepository - (SanteDB.Persistence.Data)
Represents a repository for BI assets in the database

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoBiRepository, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.BI.Services;
/// Other usings here
public class MyBiMetadataRepository : SanteDB.BI.Services.IBiMetadataRepository { 
	public String ServiceName => "My own IBiMetadataRepository service";
	/// <summary>
	/// True if the source of metadata is local
	/// </summary>
	public Boolean IsLocal {
		get;
	}
	/// <summary>
	/// Query metadata repository for
	/// </summary>
	public IEnumerable<TBisDefinition> Query<TBisDefinition>(Expression<Func<TBisDefinition,Boolean>> filter,Int32 offset,Nullable<Int32> count){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query metadata repository for
	/// </summary>
	public IQueryResultSet<TBisDefinition> Query<TBisDefinition>(Expression<Func<TBisDefinition,Boolean>> filter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified BI definition by identifier
	/// </summary>
	public TBisDefinition Get<TBisDefinition>(String id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the specified BI definition from the repository
	/// </summary>
	public void Remove<TBisDefinition>(String id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts the specified BI definition into the repository
	/// </summary>
	public TBisDefinition Insert<TBisDefinition>(TBisDefinition metadata){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBiMetadataRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_IBiMetadataRepository.htm)
* [AppletBiRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_Impl_AppletBiRepository.htm)
* [AdoBiRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoBiRepository.htm)
