---
description: IAdHocDatawarehouseService (SanteDB.Core.Api)
---

## Summary
Represents a simple data warehousing service which allows business rules to stash
            pre-computed values.

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|DataProvider|String|R|Gets the provider mnemonic|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateDatamart|DatamartDefinition|name <small style='border:solid 1px #aaa'>String</small><br/>schema <small style='border:solid 1px #aaa'>Object</small>|Creates an ad-hoc datamart which is not based on an ETL process, rather created            by a trigger.|
|GetDatamarts|List&lt;DatamartDefinition>||TODO|
|GetDatamart|DatamartDefinition|name <small style='border:solid 1px #aaa'>String</small>|Gets the specified datamart|
|GetDatamart|DatamartDefinition|id <small style='border:solid 1px #aaa'>Guid</small>|Gets the specified datamart|
|DeleteDatamart|void|datamartId <small style='border:solid 1px #aaa'>Guid</small>|Deletes a datamart|
|Truncate|void|datamartId <small style='border:solid 1px #aaa'>Guid</small>|Truncates (drops all data) the specified data mart|
|Get|Object|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>tupleId <small style='border:solid 1px #aaa'>Guid</small>|Gets data from an ad-hoc data mart|
|AdhocQuery|IEnumerable&lt;Object>|queryText <small style='border:solid 1px #aaa'>String</small>|Executes the specified query|
|AdhocQuery|IEnumerable&lt;Object>|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>filterParameters <small style='border:solid 1px #aaa'>Object</small>|Executes the specified query|
|AdhocQuery|IEnumerable&lt;Object>|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>filterParameters <small style='border:solid 1px #aaa'>Object</small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Int32</small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small>|Executes the specified query|
|CreateStoredQuery|DatamartStoredQuery|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>queryDefinition <small style='border:solid 1px #aaa'>Object</small>|Create the specified stored query on the warehouse provider|
|StoredQuery|IEnumerable&lt;Object>|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>queryId <small style='border:solid 1px #aaa'>String</small><br/>queryParameters <small style='border:solid 1px #aaa'>Object</small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Int32</small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small>|Executes a predefined query against a datamart|
|Add|Guid|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>obj <small style='border:solid 1px #aaa'>Object</small>|Adds the specified object to the specified datamart returning the tupleId|
|Delete|void|datamartId <small style='border:solid 1px #aaa'>Guid</small><br/>matchingQuery <small style='border:solid 1px #aaa'>Object</small>|Delete a tuple from the datamart|

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
	public String DataProvider {
		get;
	}
	/// <summary>
	/// Creates an ad-hoc datamart which is not based on an ETL process, rather created            by a trigger.
	/// </summary>
	public DatamartDefinition CreateDatamart(String name,Object schema){
		throw new System.NotImplementedException();
	}
	public List<DatamartDefinition> GetDatamarts(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified datamart
	/// </summary>
	public DatamartDefinition GetDatamart(String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified datamart
	/// </summary>
	public DatamartDefinition GetDatamart(Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Deletes a datamart
	/// </summary>
	public void DeleteDatamart(Guid datamartId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Truncates (drops all data) the specified data mart
	/// </summary>
	public void Truncate(Guid datamartId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets data from an ad-hoc data mart
	/// </summary>
	public Object Get(Guid datamartId,Guid tupleId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified query
	/// </summary>
	public IEnumerable<Object> AdhocQuery(String queryText){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified query
	/// </summary>
	public IEnumerable<Object> AdhocQuery(Guid datamartId,Object filterParameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified query
	/// </summary>
	public IEnumerable<Object> AdhocQuery(Guid datamartId,Object filterParameters,Int32 offset,Int32 count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create the specified stored query on the warehouse provider
	/// </summary>
	public DatamartStoredQuery CreateStoredQuery(Guid datamartId,Object queryDefinition){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes a predefined query against a datamart
	/// </summary>
	public IEnumerable<Object> StoredQuery(Guid datamartId,String queryId,Object queryParameters,Int32 offset,Int32 count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds the specified object to the specified datamart returning the tupleId
	/// </summary>
	public Guid Add(Guid datamartId,Object obj){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete a tuple from the datamart
	/// </summary>
	public void Delete(Guid datamartId,Object matchingQuery){
		throw new System.NotImplementedException();
	}
}
```
