---
description: ITemplateDefinitionRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a repository which deals with metadata such as assigning authorities,
            concept classes, etc.

## Implementations


### LocalTemplateDefinitionRepositoryService - (SanteDB.Core)
Represents a local metadata repository service

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalTemplateDefinitionRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
