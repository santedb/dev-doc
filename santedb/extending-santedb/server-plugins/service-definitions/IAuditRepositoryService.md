---
description: IAuditRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service which can persist and retrieve audits

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Insert|AuditData|*AuditData* **audit**|Insert an audit into the repository|
|Find|IEnumerable&lt;AuditData>|*Expression&lt;Func&lt;AuditData,Boolean>>* **query**|Find an audit from the audit repository|
|Get|AuditData|*Object* **correlationKey**|Get the specified audit|
|Find|IEnumerable&lt;AuditData>|*Expression&lt;Func&lt;AuditData,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*ModelSort`1[]* **orderBy**|Find an audit from the audit repository|

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
## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyAuditRepositoryService : SanteDB.Core.Security.Services.IAuditRepositoryService { 
	public String ServiceName => "My own IAuditRepositoryService service";
	/// <summary>
	/// Insert an audit into the repository
	/// </summary>
	public AuditData Insert(AuditData audit){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an audit from the audit repository
	/// </summary>
	public IEnumerable<AuditData> Find(Expression<Func<AuditData,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified audit
	/// </summary>
	public AuditData Get(Object correlationKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an audit from the audit repository
	/// </summary>
	public IEnumerable<AuditData> Find(Expression<Func<AuditData,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```
