---
description: ICarePlanService (SanteDB.Core.Api)
---

## Summary
Represents a class which can create care plans

## Implementations


### Simple Care Planning Service - (SanteDB.Core.Api)
Represents a care plan service that can bundle protocol acts together 
            based on their start/stop times

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Protocol.SimpleCarePlanService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
