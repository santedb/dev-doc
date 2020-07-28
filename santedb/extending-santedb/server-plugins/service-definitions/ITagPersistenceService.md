---
description: ITagPersistenceService (SanteDB.Core.Api)
---

## Summary
Taggable persistence service

## Implementations


### Local Tag Persistence - (SanteDB.Core)
Tag persistence service for act

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalTagPersistenceService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
