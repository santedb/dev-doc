---
description: IRecordMatchingConfigurationService (SanteDB.Core.Api)
---

## Summary
Represents a service

## Implementations


### FileMatchConfigurationProvider - (SanteDB.Matcher.Configuration.File)
Represents a configuration provider which is for matching

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Configuration.File.FileMatchConfigurationProvider, SanteDB.Matcher.Configuration.File, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### AppletMatchConfigurationProvider - (SanteDB.Matcher)
Applet match configuration provider loads match configurations from available applets

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.AppletMatchConfigurationProvider, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### AssemblyMatchConfigurationProvider - (SanteDB.Matcher)
File based match configuration provider

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.AssemblyMatchConfigurationProvider, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
