---
description: IPatientRepositoryService (SanteDB.Core.Api)
---

# Patient Repository

## Summary

Represents the patient repository service. This service is responsible for ensuring that patient roles in the IMS database are in a consistent state.

## Operations

| Operation | Response/Return | Input/Parameter                                                                               | Description                            |
| --------- | --------------- | --------------------------------------------------------------------------------------------- | -------------------------------------- |
| Merge     | Patient         | <p><em>Patient</em> <strong>survivor</strong><br><em>Patient</em> <strong>victim</strong></p> | Merges two patients together           |
| UnMerge   | Patient         | <p><em>Patient</em> <strong>patient</strong><br><em>Guid</em> <strong>versionKey</strong></p> | Un-merges two patients from each other |

## Implementations

### LocalPatientRepository - (SanteDB.Core)

Local patient repository service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalPatientRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPatientRepositoryService : SanteDB.Core.Services.IPatientRepositoryService { 
    public String ServiceName => "My own IPatientRepositoryService service";
    /// <summary>
    /// Merges two patients together
    /// </summary>
    public Patient Merge(Patient survivor,Patient victim){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Un-merges two patients from each other
    /// </summary>
    public Patient UnMerge(Patient patient,Guid versionKey){
        throw new System.NotImplementedException();
    }
}
```
