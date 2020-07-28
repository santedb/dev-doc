---
description: IAliasProvider (SanteDB.Core.Api)
---

## Summary
Represents a provider for aliases

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
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Services.ComponentAlias> GetAlias(System.String name){
		throw new System.NotImplementedException();
	}
}
```