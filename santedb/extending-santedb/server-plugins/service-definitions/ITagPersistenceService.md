---
description: ITagPersistenceService (SanteDB.Core.Api)
---

## Summary
Taggable persistence service

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Save|void|*Guid* **sourceKey**<br/>*ITag* **tag**|Save tag to source key|

## Implementations


### Local Tag Persistence - (SanteDB.Core)
Tag persistence service for act

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalTagPersistenceService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyTagPersistenceService : SanteDB.Core.Services.ITagPersistenceService { 
	public String ServiceName => "My own ITagPersistenceService service";
	/// <summary>
	/// Save tag to source key
	/// </summary>
	public void Save(Guid sourceKey,ITag tag){
		throw new System.NotImplementedException();
	}
}
```
