---
description: IPatientRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents the patient repository service. This service is responsible
            for ensuring that patient roles in the IMS database are in a consistent
            state.

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPatientRepositoryService : SanteDB.Core.Services.IPatientRepositoryService { 
	public String ServiceName => "My own IPatientRepositoryService service";
	/// <summary>
	/// Merges two patients together
	/// </summary>
	public SanteDB.Core.Model.Roles.Patient Merge(SanteDB.Core.Model.Roles.Patient survivor,SanteDB.Core.Model.Roles.Patient victim){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Un-merges two patients from each other
	/// </summary>
	public SanteDB.Core.Model.Roles.Patient UnMerge(SanteDB.Core.Model.Roles.Patient patient,System.Guid versionKey){
		throw new System.NotImplementedException();
	}
}
```
