---
description: ISqlDataPersistenceService (SanteDB.Core.Api)
---

## Summary
Represents a data persistence service where arbitrary SQL can be run

## Implementations


### ADO.NET Data Persistence Service - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySqlDataPersistenceService : SanteDB.Core.Services.ISqlDataPersistenceService { 
	public String ServiceName => "My own ISqlDataPersistenceService service";
	/// <summary>
	/// Text that identifies the type of database system that is running
	/// </summary>
	public System.String InvariantName {
		get;
	}
	/// <summary>
	/// Executes the arbitrary SQL
	/// </summary>
	public void ExecuteNonQuery(System.String sql){
		throw new System.NotImplementedException();
	}
}
```