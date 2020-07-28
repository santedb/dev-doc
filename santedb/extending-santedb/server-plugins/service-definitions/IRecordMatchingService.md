---
description: IRecordMatchingService (SanteDB.Core.Api)
---

## Summary
Represents a service that performs record matching and classification

## Implementations


### SanteMatch Deterministic Matcher - (SanteDB.Matcher)
Represents a deterministic record matching service

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Matchers.SimpleRecordMatchingService, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### SanteMatch Probabalistic Match Service - (SanteDB.Matcher)
Represents a probabalistic record matching service

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Matchers.WeightedRecordMatchingService, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
