---
description: IDataPersistenceServiceEx`1 (SanteDB.Core.Api)
---

## Summary
Extended data persistence service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Touch|void|key <small style='border:solid 1px #aaa'>System.Guid</small><br/>mode <small style='border:solid 1px #aaa'>SanteDB.Core.Services.TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Touch the specified data|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataPersistenceServiceEx<TModel> : SanteDB.Core.Services.IDataPersistenceServiceEx<TModel> { 
	public String ServiceName => "My own IDataPersistenceServiceEx`1 service";
	/// <summary>
	/// Touch the specified data
	/// </summary>
	public void Touch(System.Guid key,SanteDB.Core.Services.TransactionMode mode,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```
