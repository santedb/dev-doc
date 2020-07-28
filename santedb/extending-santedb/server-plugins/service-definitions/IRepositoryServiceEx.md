---
description: IRepositoryServiceEx<TModel> (SanteDB.Core.Api)
---

## Summary
Represents a repository service wrapping an extended persistence service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Touch|void|*Guid* **key**|Touch the specified object|
|Nullify|TModel|*Guid* **id**|Nullifies a specific instance|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRepositoryServiceEx<TModel> : SanteDB.Core.Services.IRepositoryServiceEx<TModel> { 
	public String ServiceName => "My own IRepositoryServiceEx`1 service";
	/// <summary>
	/// Touch the specified object
	/// </summary>
	public void Touch(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Nullifies a specific instance
	/// </summary>
	public TModel Nullify(Guid id){
		throw new System.NotImplementedException();
	}
}
```
