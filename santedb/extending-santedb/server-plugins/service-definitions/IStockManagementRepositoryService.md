---
description: IStockManagementRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a stock management repository service.

## Implementations


### Local Stock Management Repository - (SanteDB.Core)
Represents a stock management repository service.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalStockManagementRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
