---
description: IBiMetadataRepository (SanteDB.BI)
---

## Summary
Represents a metadata repository for the BIS services

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Query|System.Collections.Generic.IEnumerable&lt;TBisDefinition>|filter <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TBisDefinition,System.Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small>|Query metadata repository for|
|Get|TBisDefinition|id <small style='border:solid 1px #aaa'>System.String</small>|Get the specified BI definition by identifier|
|Remove|void|id <small style='border:solid 1px #aaa'>System.String</small>|Removes the specified BI definition from the repository|
|Insert|TBisDefinition|metadata <small style='border:solid 1px #aaa'>TBisDefinition</small>|Inserts the specified BI definition into the repository|

## Implementations


### AppletBiRepository - (SanteDB.BI)
Represents a default implementation of a BIS metadata repository which loads definitions from loaded applets

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.AppletBiRepository, SanteDB.BI, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### File Based BI Repository - (SanteDB.Tools.Debug)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Tools.Debug.BI.FileMetadataRepository, SanteDB.Tools.Debug, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.BI.Services;
/// Other usings here
public class MyBiMetadataRepository : SanteDB.BI.Services.IBiMetadataRepository { 
	public String ServiceName => "My own IBiMetadataRepository service";
	/// <summary>
	/// Query metadata repository for
	/// </summary>
	public System.Collections.Generic.IEnumerable<TBisDefinition> Query<TBisDefinition>(System.Linq.Expressions.Expression<System.Func<TBisDefinition,System.Boolean>> filter,System.Int32 offset,System.Nullable<System.Int32> count){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified BI definition by identifier
	/// </summary>
	public TBisDefinition Get<TBisDefinition>(System.String id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the specified BI definition from the repository
	/// </summary>
	public void Remove<TBisDefinition>(System.String id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts the specified BI definition into the repository
	/// </summary>
	public TBisDefinition Insert<TBisDefinition>(TBisDefinition metadata){
		throw new System.NotImplementedException();
	}
}
```
