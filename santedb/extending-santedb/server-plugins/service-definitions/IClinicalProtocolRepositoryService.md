---
description: IClinicalProtocolRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service that can do clinical protocols

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyClinicalProtocolRepositoryService : SanteDB.Core.Services.IClinicalProtocolRepositoryService { 
	public String ServiceName => "My own IClinicalProtocolRepositoryService service";
	/// <summary>
	/// Find protocols in the repository service
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.Acts.Protocol> FindProtocol(System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Model.Acts.Protocol,System.Boolean>> predicate,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find protocols in the repository service
	/// </summary>
	public SanteDB.Core.Model.Acts.Protocol InsertProtocol(SanteDB.Core.Model.Acts.Protocol data){
		throw new System.NotImplementedException();
	}
}
```
