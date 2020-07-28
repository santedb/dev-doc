---
description: IPolicyInformationService (SanteDB.Core.Api)
---

## Summary
Represents a contract for a policy information service

## Implementations


### ADO.NET Policy Information Service - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPolicyInformationService, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
