---
description: IAdhocCacheService (SanteDB.Core.Api)
---

## Summary
A caching service which permits the storage of any data regardless of type

## Implementations


### RedisAdhocCache - (SanteDB.Caching.Redis)
TODO: Document this

#### Service Registration
```
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisAdhocCache, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```
None
```
