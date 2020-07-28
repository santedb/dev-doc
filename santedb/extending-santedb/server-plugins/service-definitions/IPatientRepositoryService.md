---
description: IPatientRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents the patient repository service. This service is responsible
            for ensuring that patient roles in the IMS database are in a consistent
            state.

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
