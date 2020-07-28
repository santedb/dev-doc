---
description: IConceptRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service which is responsible for the maintenance of concepts.

## Implementations


### LocalConceptRepository - (SanteDB.Core)
Represents a service which is responsible for the
            maintenance of concepts.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalConceptRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
