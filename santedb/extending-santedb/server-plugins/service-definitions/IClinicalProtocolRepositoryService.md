---
description: IClinicalProtocolRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service that can do clinical protocols

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindProtocol|IEnumerable&lt;Protocol>|predicate <small style='border:solid 1px #aaa'>Expression<Func<Protocol,Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small>|Find protocols in the repository service|
|InsertProtocol|Protocol|data <small style='border:solid 1px #aaa'>Protocol</small>|Find protocols in the repository service|

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
	public IEnumerable<Protocol> FindProtocol(Expression<Func<Protocol,Boolean>> predicate,Int32 offset,Nullable<Int32> count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find protocols in the repository service
	/// </summary>
	public Protocol InsertProtocol(Protocol data){
		throw new System.NotImplementedException();
	}
}
```
