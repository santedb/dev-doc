---
description: IMailMessageRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents an alerting service.

## Implementations


### Local Mail Message - (SanteDB.Core)
Represents a local alert service.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalMailMessageRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
