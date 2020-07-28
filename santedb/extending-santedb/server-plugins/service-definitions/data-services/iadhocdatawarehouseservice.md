---
description: IAdHocDatawarehouseService (SanteDB.Core.Api)
---

# Adhoc Data Warehouse

## Summary

Represents a simple data warehousing service which allows business rules to stash pre-computed values.

## Properties

| Property | Type | Access | Description |
| :--- | :--- | :--- | :--- |
| DataProvider | String | R | Gets the provider mnemonic |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| CreateDatamart | DatamartDefinition | _String_ **name** _Object_ **schema** | Creates an ad-hoc datamart which is not based on an ETL process, rather created            by a trigger. |
| GetDatamarts | List&lt;DatamartDefinition&gt; |  | TODO |
| GetDatamart | DatamartDefinition | _String_ **name** | Gets the specified datamart |
| GetDatamart | DatamartDefinition | _Guid_ **id** | Gets the specified datamart |
| DeleteDatamart | void | _Guid_ **datamartId** | Deletes a datamart |
| Truncate | void | _Guid_ **datamartId** | Truncates \(drops all data\) the specified data mart |
| Get | Object | _Guid_ **datamartId** _Guid_ **tupleId** | Gets data from an ad-hoc data mart |
| AdhocQuery | IEnumerable&lt;Object&gt; | _String_ **queryText** | Executes the specified query |
| AdhocQuery | IEnumerable&lt;Object&gt; | _Guid_ **datamartId** _Object_ **filterParameters** | Executes the specified query |
| AdhocQuery | IEnumerable&lt;Object&gt; | _Guid_ **datamartId** _Object_ **filterParameters** _Int32_ **offset** _Int32_ **count** _Int32&_ **totalResults** | Executes the specified query |
| CreateStoredQuery | DatamartStoredQuery | _Guid_ **datamartId** _Object_ **queryDefinition** | Create the specified stored query on the warehouse provider |
| StoredQuery | IEnumerable&lt;Object&gt; | _Guid_ **datamartId** _String_ **queryId** _Object_ **queryParameters** _Int32_ **offset** _Int32_ **count** _Int32&_ **totalResults** | Executes a predefined query against a datamart |
| Add | Guid | _Guid_ **datamartId** _Object_ **obj** | Adds the specified object to the specified datamart returning the tupleId |
| Delete | void | _Guid_ **datamartId** _Object_ **matchingQuery** | Delete a tuple from the datamart |

## Implementations

### ADO.NET Ad-Hoc Data Warehouse Service - \(SanteDB.Warehouse.ADO\)

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

## Example Implementation

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

