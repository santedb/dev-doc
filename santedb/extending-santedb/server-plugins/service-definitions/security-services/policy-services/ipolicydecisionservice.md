---
description: IPolicyDecisionService (SanteDB.Core.Api)
---

# Policy Decision Service

## Summary

Represents a policy decision service

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| GetPolicyDecision | PolicyDecision | _IPrincipal_ **principal** _Object_ **securable** | Make a simple policy decision for a specific securable |
| GetPolicyOutcome | PolicyGrantType | _IPrincipal_ **principal** _String_ **policyId** | Get a policy decision outcome \(i.e. make a policy decision\) |

## Implementations

### Default PDP Service - \(SanteDB.Core\)

Local policy decision service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Security.DefaultPolicyDecisionService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPolicyDecisionService : SanteDB.Core.Security.Services.IPolicyDecisionService { 
    public String ServiceName => "My own IPolicyDecisionService service";
    /// <summary>
    /// Make a simple policy decision for a specific securable
    /// </summary>
    public PolicyDecision GetPolicyDecision(IPrincipal principal,Object securable){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get a policy decision outcome (i.e. make a policy decision)
    /// </summary>
    public PolicyGrantType GetPolicyOutcome(IPrincipal principal,String policyId){
        throw new System.NotImplementedException();
    }
}
```

