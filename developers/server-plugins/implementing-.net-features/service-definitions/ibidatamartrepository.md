`IBiDatamartRepository` in assembly SanteDB.BI version 3.0.1980.0

# Summary
Represents a BI datamart registry which contains metadata about the various
            BI datamarts that exist in the SanteDB deployment.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Find|IQueryResultSet&lt;IDatamart>|*Expression&lt;Func&lt;IDatamart,Boolean>>* **query**|Gets the datamarts which are configured with this manager|
|Register|IDatamart|*BiDatamartDefinition* **dataMartDefinition**|Create a new BI datamart based on|
|Unregister|void|*IDatamart* **datamart**|Removes the  from the manager|
|GetExecutionContext|IDataFlowExecutionContext|*IDatamart* **datamart**<br/>*DataFlowExecutionPurposeType* **purpose**|Begins the refresh process for the datamart object|

# Implementations


## AdoBiDatamartRepository - (SanteDB.Persistence.Data)
Represents an implementation of the BI datamart manager which uses the primary ADO storage to store 
            metadata about the other datamarts which are available on the SanteDB server

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoBiDatamartRepository, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.BI.Services;
/// Other usings here
public class MyBiDatamartRepository : SanteDB.BI.Services.IBiDatamartRepository { 
	public String ServiceName => "My own IBiDatamartRepository service";
	/// <summary>
	/// Gets the datamarts which are configured with this manager
	/// </summary>
	public IQueryResultSet<IDatamart> Find(Expression<Func<IDatamart,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a new BI datamart based on
	/// </summary>
	public IDatamart Register(BiDatamartDefinition dataMartDefinition){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the  from the manager
	/// </summary>
	public void Unregister(IDatamart datamart){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Begins the refresh process for the datamart object
	/// </summary>
	public IDataFlowExecutionContext GetExecutionContext(IDatamart datamart,DataFlowExecutionPurposeType purpose){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBiDatamartRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_IBiDatamartRepository.htm)
* [AdoBiDatamartRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoBiDatamartRepository.htm)
