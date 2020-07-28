---
description: INetworkInformationService (SanteDB.Core.Api)
---

## Summary
Represents network information service

## Implementations


### Default Network Information Service - (SanteDB.Core)
Default network information service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultNetworkInformationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
