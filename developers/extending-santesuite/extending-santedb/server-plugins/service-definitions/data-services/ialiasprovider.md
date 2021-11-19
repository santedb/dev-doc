---
description: IAliasProvider (SanteDB.Core.Api)
---

# Alias Provider

## Summary

Represents a provider for aliases

## Operations

| Operation | Response/Return              | Input/Parameter   | Description                                        |
| --------- | ---------------------------- | ----------------- | -------------------------------------------------- |
| GetAlias  | IEnumerable\<ComponentAlias> | _String_ **name** | Gets the known alias names and score for the alias |

## Implementations

None

## Example Implementation

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
