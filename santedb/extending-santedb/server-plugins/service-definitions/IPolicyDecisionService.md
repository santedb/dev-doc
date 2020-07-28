---
description: IPolicyDecisionService (SanteDB.Core.Api)
---

## Summary
Represents a policy decision service

## Implementations


### Default PDP Service - (SanteDB.Core)
Local policy decision service

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultPolicyDecisionService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
