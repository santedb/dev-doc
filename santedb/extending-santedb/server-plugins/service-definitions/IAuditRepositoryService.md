---
description: IAuditRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service which can persist and retrieve audits

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Insert|SanteDB.Core.Auditing.AuditData|audit <small style='border:solid 1px #aaa'>SanteDB.Core.Auditing.AuditData</small>|Insert an audit into the repository|
|Find|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Auditing.AuditData>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Auditing.AuditData,System.Boolean>></small>|Find an audit from the audit repository|
|Get|SanteDB.Core.Auditing.AuditData|correlationKey <small style='border:solid 1px #aaa'>System.Object</small>|Get the specified audit|
|Find|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Auditing.AuditData>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Auditing.AuditData,System.Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>System.Int32&</small><br/>orderBy <small style='border:solid 1px #aaa'>SanteDB.Core.Model.Query.ModelSort`1[[SanteDB.Core.Auditing.AuditData, SanteDB.Core.Model, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null]][]</small>|Find an audit from the audit repository|

## Implementations


### Default Audit Repository - (SanteDB.Core)
Represents an audit repository which stores and queries audit data.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalAuditRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyAuditRepositoryService : SanteDB.Core.Security.Services.IAuditRepositoryService { 
	public String ServiceName => "My own IAuditRepositoryService service";
	/// <summary>
	/// Insert an audit into the repository
	/// </summary>
	public SanteDB.Core.Auditing.AuditData Insert(SanteDB.Core.Auditing.AuditData audit){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an audit from the audit repository
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Auditing.AuditData> Find(System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Auditing.AuditData,System.Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified audit
	/// </summary>
	public SanteDB.Core.Auditing.AuditData Get(System.Object correlationKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an audit from the audit repository
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Auditing.AuditData> Find(System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Auditing.AuditData,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,SanteDB.Core.Model.Query.ModelSort`1[[SanteDB.Core.Auditing.AuditData, SanteDB.Core.Model, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null]][] orderBy){
		throw new System.NotImplementedException();
	}
}
```
