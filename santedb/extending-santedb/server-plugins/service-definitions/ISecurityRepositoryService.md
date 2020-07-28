---
description: ISecurityRepositoryService (SanteDB.Core.Api)
---

## Summary
Security repository service is responsible for the maintenance of security entities

## Implementations


### LocalSecurityRepositoryService - (SanteDB.Core)
Represents a security repository service that uses the direct local services

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalSecurityRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
