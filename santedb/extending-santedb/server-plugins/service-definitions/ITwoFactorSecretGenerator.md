---
description: ITwoFactorSecretGenerator (SanteDB.Core.Api)
---

## Summary
Identifies a class which can generate TFA secrets

## Implementations


### Simple TFA Secret Generator - (SanteDB.Core)
Represents a TFA secret generator which uses the server's clock

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SimpleTfaSecretGenerator, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
