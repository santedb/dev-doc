---
description: IValidatingRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Represents a repository that can validate

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Validate|TModel|data <small style='border:solid 1px #aaa'>TModel</small>|Validates the supplied data and returns a valid copy (or) throws an appropriate exception|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyValidatingRepositoryService<TModel> : SanteDB.Core.Services.IValidatingRepositoryService<TModel> { 
	public String ServiceName => "My own IValidatingRepositoryService`1 service";
	/// <summary>
	/// Validates the supplied data and returns a valid copy (or) throws an appropriate exception
	/// </summary>
	public TModel Validate(TModel data){
		throw new System.NotImplementedException();
	}
}
```
