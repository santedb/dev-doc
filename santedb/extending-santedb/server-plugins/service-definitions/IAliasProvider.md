---
description: IAliasProvider (SanteDB.Core.Api)
---

## Summary
Represents a provider for aliases

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetAlias|IEnumerable&lt;ComponentAlias>|name <small style='border:solid 1px #aaa'>String</small>|Gets the known alias names and score for the alias|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAliasProvider : SanteDB.Core.Services.IAliasProvider { 
	public String ServiceName => "My own IAliasProvider service";
	/// <summary>
	/// Gets the known alias names and score for the alias
	/// </summary>
	public IEnumerable<ComponentAlias> GetAlias(String name){
		throw new System.NotImplementedException();
	}
}
```
