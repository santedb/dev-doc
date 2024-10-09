`IBiDatamartManager` in assembly SanteDB.BI version 3.0.1980.0

# Summary
Represents a flow executor

# Events

|Event|Type|Description|
|-|-|-|
|DiagnosticEventReceived|EventHandler|Fired after a diagnostic sample was received|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Migrate|void|*BiDatamartDefinition* **datamartDefinition**|Migrate the datamart schema specified by|
|Refresh|IDataFlowDiagnosticSession|*BiDatamartDefinition* **datamartDefinition**<br/>*Boolean* **includeDiagnostics**|Refresh the datamart specified by|
|Destroy|void|*BiDatamartDefinition* **datamartDefinition**|Destroy the datamart data|

# Implementations


## DefaultDatamartManager - (SanteDB.BI)
Default datamart manager

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.DefaultDatamartManager, SanteDB.BI, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.BI.Services;
/// Other usings here
public class MyBiDatamartManager : SanteDB.BI.Services.IBiDatamartManager { 
	public String ServiceName => "My own IBiDatamartManager service";
	/// <summary>
	/// Fired after a diagnostic sample was received
	/// </summary>
	public event EventHandler DiagnosticEventReceived;
	/// <summary>
	/// Migrate the datamart schema specified by
	/// </summary>
	public void Migrate(BiDatamartDefinition datamartDefinition){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Refresh the datamart specified by
	/// </summary>
	public IDataFlowDiagnosticSession Refresh(BiDatamartDefinition datamartDefinition,Boolean includeDiagnostics){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Destroy the datamart data
	/// </summary>
	public void Destroy(BiDatamartDefinition datamartDefinition){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBiDatamartManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_IBiDatamartManager.htm)
* [DefaultDatamartManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_Impl_DefaultDatamartManager.htm)
