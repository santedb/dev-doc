---
description: IDataSigningService (SanteDB.Core.Api)
---

# Data Signing Service

## Summary

Represents a service which can sign arbitrary data

## Operations

| Operation             | Response/Return | Input/Parameter                                                                                                                      | Description                                                                    |
| --------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| GetSignatureAlgorithm | String          | _String_ **keyId**                                                                                                                   | Get the siganture algorithm this service would use to sign w/the specified key |
| SignData              | Byte\[]         | <p><em>Byte[]</em> <strong>data</strong><br><em>String</em> <strong>keyId</strong></p>                                               | Signs the specified data using the service's configured signing key            |
| Verify                | Boolean         | <p><em>Byte[]</em> <strong>data</strong><br><em>Byte[]</em> <strong>signature</strong><br><em>String</em> <strong>keyId</strong></p> | Verifies the digital signature of the data                                     |

## Implementations

### DefaultDataSigningService - (SanteDB.Core)

Default data signature service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Security.DefaultDataSigningService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MyDataSigningService : SanteDB.Core.Security.IDataSigningService { 
    public String ServiceName => "My own IDataSigningService service";
    /// <summary>
    /// Get the siganture algorithm this service would use to sign w/the specified key
    /// </summary>
    public String GetSignatureAlgorithm(String keyId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Signs the specified data using the service's configured signing key
    /// </summary>
    public Byte[] SignData(Byte[] data,String keyId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Verifies the digital signature of the data
    /// </summary>
    public Boolean Verify(Byte[] data,Byte[] signature,String keyId){
        throw new System.NotImplementedException();
    }
}
```
