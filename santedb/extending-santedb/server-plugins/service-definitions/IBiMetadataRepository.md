---
description: IBiMetadataRepository (SanteDB.BI)
---

## Summary
Represents a metadata repository for the BIS services

## Implementations


### AppletBiRepository - (SanteDB.BI)
Represents a default implementation of a BIS metadata repository which loads definitions from loaded applets

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.AppletBiRepository, SanteDB.BI, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### File Based BI Repository - (SanteDB.Tools.Debug)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Tools.Debug.BI.FileMetadataRepository, SanteDB.Tools.Debug, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
