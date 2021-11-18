---
description: IPasswordValidatorService (SanteDB.Core.Api)
---

# Password Validation Service

## Summary

Represents a password validation service

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Validate | Boolean | _String_ **password** | Validate the password |

## Implementations

### Default Password Validator - \(SanteDB.Core\)

Represents a local regex password validator

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Security.DefaultPasswordValidationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPasswordValidatorService : SanteDB.Core.Security.Services.IPasswordValidatorService { 
    public String ServiceName => "My own IPasswordValidatorService service";
    /// <summary>
    /// Validate the password
    /// </summary>
    public Boolean Validate(String password){
        throw new System.NotImplementedException();
    }
}
```

