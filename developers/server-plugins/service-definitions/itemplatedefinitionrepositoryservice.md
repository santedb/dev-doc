---
description: ITemplateDefinitionRepositoryService (SanteDB.Core.Api)
---

# Template Definition Repository

## Summary

Represents a repository which deals with metadata such as assigning authorities, concept classes, etc.

## Operations

| Operation             | Response/Return    | Input/Parameter       | Description            |
| --------------------- | ------------------ | --------------------- | ---------------------- |
| GetTemplateDefinition | TemplateDefinition | _String_ **mnemonic** | Get tempate definition |

## Implementations

### LocalTemplateDefinitionRepositoryService - (SanteDB.Core)

Represents a local metadata repository service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalTemplateDefinitionRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyTemplateDefinitionRepositoryService : SanteDB.Core.Services.ITemplateDefinitionRepositoryService { 
    public String ServiceName => "My own ITemplateDefinitionRepositoryService service";
    /// <summary>
    /// Get tempate definition
    /// </summary>
    public TemplateDefinition GetTemplateDefinition(String mnemonic){
        throw new System.NotImplementedException();
    }
}
```
