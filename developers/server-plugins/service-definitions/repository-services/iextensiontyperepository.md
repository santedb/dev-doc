---
description: IExtensionTypeRepository (SanteDB.Core.Api)
---

# Extension Type Repository

## Summary

Represents the extension type repository

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Get | ExtensionType | _Uri_ **uri** | Get the xtension type my its url |

## Implementations

### LocalExtensionTypeRepository - \(SanteDB.Core\)

Local extension types

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalExtensionTypeRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyExtensionTypeRepository : SanteDB.Core.Services.IExtensionTypeRepository { 
    public String ServiceName => "My own IExtensionTypeRepository service";
    /// <summary>
    /// Get the xtension type my its url
    /// </summary>
    public ExtensionType Get(Uri uri){
        throw new System.NotImplementedException();
    }
}
```

