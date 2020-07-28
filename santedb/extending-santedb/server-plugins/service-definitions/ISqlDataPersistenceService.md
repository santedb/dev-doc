---
description: ISqlDataPersistenceService (SanteDB.Core.Api)
---

## Summary
Represents a data persistence service where arbitrary SQL can be run

## Implementations


### ADO.NET Data Persistence Service - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
