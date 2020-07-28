---
description: IExtensionTypeRepository (SanteDB.Core.Api)
---

## Summary
Represents the extension type repository

## Implementations


### LocalExtensionTypeRepository - (SanteDB.Core)
Local extension types

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalExtensionTypeRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
