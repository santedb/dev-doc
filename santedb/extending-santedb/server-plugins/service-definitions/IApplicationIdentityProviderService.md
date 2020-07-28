---
description: IApplicationIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Represents a service which retrieves IPrincipal objects for applications.

## Implementations


### ADO.NET Application Identity Provider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoApplicationIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
