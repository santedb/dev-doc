---
description: IJobManagerService (SanteDB.Core.Api)
---

## Summary
Job manager service

## Implementations


### Default Job Manager - (SanteDB.Core)
Represents the default implementation of the timer

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.DefaultJobManagerService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
