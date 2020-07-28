---
description: IRepositoryServiceFactory (SanteDB.Core.Api)
---

## Summary
Represents a factory service which can be used to generate default factories

## Implementations


### Local Data Repository Factory - (SanteDB.Core)
Represents a generic resource repository factory

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalRepositoryFactoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
