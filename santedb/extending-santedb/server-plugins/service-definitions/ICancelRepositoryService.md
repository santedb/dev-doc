---
description: ICancelRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Represents a repository that can cancel an act

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCancelRepositoryService<TModel> : SanteDB.Core.Services.ICancelRepositoryService<TModel> { 
	public String ServiceName => "My own ICancelRepositoryService`1 service";
	/// <summary>
	/// Cancels the specified object
	/// </summary>
	public TModel Cancel(System.Guid id){
		throw new System.NotImplementedException();
	}
}
```
