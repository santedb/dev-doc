---
description: IPatchService (SanteDB.Core.Api)
---

# Patch Service

## Summary

Represents a patch service which can calculate and apply patches

## Operations

| Operation | Response/Return | Input/Parameter                                                                                                                                                     | Description                                                                              |
| --------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Diff      | Patch           | <p><em>IdentifiedData</em> <strong>existing</strong><br><em>IdentifiedData</em> <strong>updated</strong><br><em>String[]</em> <strong>ignoreProperties</strong></p> | Performs a DIFF and creates the related patch which can be used to update             to |
| Patch     | IdentifiedData  | <p><em>Patch</em> <strong>patch</strong><br><em>IdentifiedData</em> <strong>data</strong><br><em>Boolean</em> <strong>force</strong></p>                            | Apples the specified  onto  returning the updated object                                 |
| Test      | Boolean         | <p><em>Patch</em> <strong>patch</strong><br><em>IdentifiedData</em> <strong>target</strong></p>                                                                     | Tests that the patch can be applied on the specified object                              |

## Implementations

### Basic Patching Service - (SanteDB.Core.Api)

Represents a simple patch service which can calculate patches and apply them

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.SimplePatchService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPatchService : SanteDB.Core.Services.IPatchService { 
    public String ServiceName => "My own IPatchService service";
    /// <summary>
    /// Performs a DIFF and creates the related patch which can be used to update             to
    /// </summary>
    public Patch Diff(IdentifiedData existing,IdentifiedData updated,String[] ignoreProperties){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Apples the specified  onto  returning the updated object
    /// </summary>
    public IdentifiedData Patch(Patch patch,IdentifiedData data,Boolean force){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Tests that the patch can be applied on the specified object
    /// </summary>
    public Boolean Test(Patch patch,IdentifiedData target){
        throw new System.NotImplementedException();
    }
}
```
