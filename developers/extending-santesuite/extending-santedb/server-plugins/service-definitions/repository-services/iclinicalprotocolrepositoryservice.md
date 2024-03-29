---
description: IClinicalProtocolRepositoryService (SanteDB.Core.Api)
---

# Clinical Protocol Repository

## Summary

Represents a service that can do clinical protocols

## Operations

| Operation      | Response/Return        | Input/Parameter                                                                                                                                                                                                                                 | Description                              |
| -------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| FindProtocol   | IEnumerable\<Protocol> | <p><em>Expression&#x3C;Func&#x3C;Protocol,Boolean>></em> <strong>predicate</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong></p> | Find protocols in the repository service |
| InsertProtocol | Protocol               | _Protocol_ **data**                                                                                                                                                                                                                             | Find protocols in the repository service |

## Implementations

### Applet Based Clinical Protocol Repository - (SanteDB.Cdss.Xml)

Applet clinical protocol repository

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Cdss.Xml.AppletClinicalProtocolRepository, SanteDB.Cdss.Xml, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyClinicalProtocolRepositoryService : SanteDB.Core.Services.IClinicalProtocolRepositoryService { 
    public String ServiceName => "My own IClinicalProtocolRepositoryService service";
    /// <summary>
    /// Find protocols in the repository service
    /// </summary>
    public IEnumerable<Protocol> FindProtocol(Expression<Func<Protocol,Boolean>> predicate,Int32 offset,Nullable<Int32> count,Int32& totalResults){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Find protocols in the repository service
    /// </summary>
    public Protocol InsertProtocol(Protocol data){
        throw new System.NotImplementedException();
    }
}
```
