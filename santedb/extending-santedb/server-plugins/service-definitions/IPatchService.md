---
description: IPatchService (SanteDB.Core.Api)
---

## Summary
Represents a patch service which can calculate and apply patches

## Implementations


### Basic Patching Service - (SanteDB.Core.Api)
Represents a simple patch service which can calculate patches and apply them

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.SimplePatchService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
