---
description: IDataSigningService (SanteDB.Core.Api)
---

## Summary
Represents a service which can sign arbitrary data

## Implementations


### DefaultDataSigningService - (SanteDB.Core)
Default data signature service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultDataSigningService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
