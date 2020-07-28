---
description: IBiRenderService (SanteDB.BI)
---

## Summary
BI Render service

## Implementations


### LocalBiRenderService - (SanteDB.BI)
Rendering service which renders reports locally

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.LocalBiRenderService, SanteDB.BI, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
