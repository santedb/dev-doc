---
description: IPasswordValidatorService (SanteDB.Core.Api)
---

## Summary
Represents a password validation service

## Implementations


### Default Password Validator - (SanteDB.Core)
Represents a local regex password validator

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultPasswordValidationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
