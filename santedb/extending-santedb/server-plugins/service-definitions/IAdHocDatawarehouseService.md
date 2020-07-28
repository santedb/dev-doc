---
description: IAdHocDatawarehouseService (SanteDB.Core.Api)
---

## Summary
Represents a simple data warehousing service which allows business rules to stash
            pre-computed values.

## Implementations


### ADO.NET Ad-Hoc Data Warehouse Service - (SanteDB.Warehouse.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Warehouse.ADO.ADODataWarehouse, SanteDB.Warehouse.ADO, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAdHocDatawarehouseService : SanteDB.Core.Services.IAdHocDatawarehouseService { 
	public String ServiceName => "My own IAdHocDatawarehouseService service";
	/// <summary>
	/// Gets the provider mnemonic
	/// </summary>
	public System.String DataProvider {
		get;
	}
	/// <summary>
	/// Creates an ad-hoc datamart which is not based on an ETL process, rather created            by a trigger.
	/// </summary>
	public SanteDB.Core.Model.Warehouse.DatamartDefinition CreateDatamart(System.String name,System.Object schema){
		throw new System.NotImplementedException();
	}
	public System.Collections.Generic.List<SanteDB.Core.Model.Warehouse.DatamartDefinition> GetDatamarts(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified datamart
	/// </summary>
	public SanteDB.Core.Model.Warehouse.DatamartDefinition GetDatamart(System.String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified datamart
	/// </summary>
	public SanteDB.Core.Model.Warehouse.DatamartDefinition GetDatamart(System.Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Deletes a datamart
	/// </summary>
	public void DeleteDatamart(System.Guid datamartId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Truncates (drops all data) the specified data mart
	/// </summary>
	public void Truncate(System.Guid datamartId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets data from an ad-hoc data mart
	/// </summary>
	public System.Object Get(System.Guid datamartId,System.Guid tupleId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified query
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Object> AdhocQuery(System.String queryText){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified query
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Object> AdhocQuery(System.Guid datamartId,System.Object filterParameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified query
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Object> AdhocQuery(System.Guid datamartId,System.Object filterParameters,System.Int32 offset,System.Int32 count,System.Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create the specified stored query on the warehouse provider
	/// </summary>
	public SanteDB.Core.Model.Warehouse.DatamartStoredQuery CreateStoredQuery(System.Guid datamartId,System.Object queryDefinition){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes a predefined query against a datamart
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Object> StoredQuery(System.Guid datamartId,System.String queryId,System.Object queryParameters,System.Int32 offset,System.Int32 count,System.Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds the specified object to the specified datamart returning the tupleId
	/// </summary>
	public System.Guid Add(System.Guid datamartId,System.Object obj){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete a tuple from the datamart
	/// </summary>
	public void Delete(System.Guid datamartId,System.Object matchingQuery){
		throw new System.NotImplementedException();
	}
}
```