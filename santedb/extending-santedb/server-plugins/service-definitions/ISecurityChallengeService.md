---
description: ISecurityChallengeService (SanteDB.Core.Api)
---

## Summary
Represents an interface that allows for the retrieval of pre-configured security challenges

## Implementations


### AdoSecurityChallengeProvider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSecurityChallengeProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
