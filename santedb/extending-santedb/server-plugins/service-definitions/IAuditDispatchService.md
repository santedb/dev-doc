---
description: IAuditDispatchService (SanteDB.Core.Api)
---

## Summary
Represents a service that dispatches audits to a central repository

## Implementations


### IHE ATNA Audit Dispatcher - (SanteDB.Messaging.Atna)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.Atna.AtnaAuditService, SanteDB.Messaging.Atna, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
