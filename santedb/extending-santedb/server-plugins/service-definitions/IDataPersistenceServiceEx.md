---
description: IDataPersistenceServiceEx<TModel> (SanteDB.Core.Api)
---

## Summary
Extended data persistence service

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Touch|void|*Guid* **key**<br/>*TransactionMode* **mode**<br/>*IPrincipal* **principal**|Touch the specified data|

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
	public void Touch(Guid key,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```
