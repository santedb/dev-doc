---
description: IElevatableIdentityProviderService (SanteDB.Core.Api)
---

# Elevating Identity Provider Service

## Summary

Represents an identity provider that allows for elevation

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| OverrideRequested | EventHandler&lt;SecurityOverrideEventArgs&gt; | The caller has requested an override |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| ElevatedAuthenticate | IPrincipal | _String_ **userName** _String_ **password** _String_ **tfaSecret** _String_ **purpose** _String\[\]_ **policies** | Requests the currently established principal to be elevated |

## Implementations

None

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyElevatableIdentityProviderService : SanteDB.Core.Security.Services.IElevatableIdentityProviderService { 
    public String ServiceName => "My own IElevatableIdentityProviderService service";
    /// <summary>
    /// The caller has requested an override
    /// </summary>
    public event EventHandler<SecurityOverrideEventArgs> OverrideRequested;
    /// <summary>
    /// Requests the currently established principal to be elevated
    /// </summary>
    public IPrincipal ElevatedAuthenticate(String userName,String password,String tfaSecret,String purpose,String[] policies){
        throw new System.NotImplementedException();
    }
}
```

