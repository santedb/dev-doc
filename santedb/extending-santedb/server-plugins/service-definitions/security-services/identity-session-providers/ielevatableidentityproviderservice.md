---
description: IElevatableIdentityProviderService (SanteDB.Core.Api)
---

# Elevating Identity Provider Service

## Summary

Represents an identity provider that allows for elevation

## Events

| Event             | Type                                     | Description                          |
| ----------------- | ---------------------------------------- | ------------------------------------ |
| OverrideRequested | EventHandler\<SecurityOverrideEventArgs> | The caller has requested an override |

## Operations

| Operation            | Response/Return | Input/Parameter                                                                                                                                                                                                                        | Description                                                 |
| -------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| ElevatedAuthenticate | IPrincipal      | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>password</strong><br><em>String</em> <strong>tfaSecret</strong><br><em>String</em> <strong>purpose</strong><br><em>String[]</em> <strong>policies</strong></p> | Requests the currently established principal to be elevated |

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
