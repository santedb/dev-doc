---
description: ISubscriptionExecutor (SanteDB.Core.Api)
---

## Summary
Represents a subscription executor

## Implementations


### ADO.NET Subscription Executor - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSubscriptionExector, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
