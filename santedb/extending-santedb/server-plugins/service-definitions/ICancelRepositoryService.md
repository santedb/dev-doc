---
description: ICancelRepositoryService<TModel> (SanteDB.Core.Api)
---

## Summary
Represents a repository that can cancel an act

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Cancel|TModel|id <small style='border:solid 1px #aaa'>Guid</small>|Cancels the specified object|

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
	public TModel Cancel(Guid id){
		throw new System.NotImplementedException();
	}
}
```
