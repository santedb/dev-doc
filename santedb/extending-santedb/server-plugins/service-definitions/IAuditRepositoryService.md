---
description: IAuditRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service which can persist and retrieve audits

## Implementations


### Default Audit Repository - (SanteDB.Core)
Represents an audit repository which stores and queries audit data.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalAuditRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
