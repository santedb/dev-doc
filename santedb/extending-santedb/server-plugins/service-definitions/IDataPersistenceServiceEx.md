---
description: IDataPersistenceServiceEx`1 (SanteDB.Core.Api)
---

## Summary
Extended data persistence service

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
