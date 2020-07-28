---
description: IClinicalProtocolRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service that can do clinical protocols

## Implementations


### Applet Based Clinical Protocol Repository - (SanteDB.Cdss.Xml)
Applet clinical protocol repository

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Cdss.Xml.AppletClinicalProtocolRepository, SanteDB.Cdss.Xml, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
