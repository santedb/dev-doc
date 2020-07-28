---
description: ISubscriptionExecutor (SanteDB.Core.Api)
---

## Summary
Represents a subscription executor

## Implementations


### ADO.NET Subscription Executor - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSubscriptionExector, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySubscriptionExecutor : SanteDB.Core.Services.ISubscriptionExecutor { 
	public String ServiceName => "My own ISubscriptionExecutor service";
	/// <summary>
	/// Occurs when queried.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.QueryResultEventArgs<SanteDB.Core.Model.IdentifiedData>> Executed;
	/// <summary>
	/// Occurs when querying.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.QueryRequestEventArgs<SanteDB.Core.Model.IdentifiedData>> Executing;
	/// <summary>
	/// Executes the specified subscription mechanism
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Object> Execute(System.Guid subscriptionKey,SanteDB.Core.Model.Query.NameValueCollection parameters,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified subscription mechanism
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Object> Execute(SanteDB.Core.Model.Subscription.SubscriptionDefinition subscription,SanteDB.Core.Model.Query.NameValueCollection parameters,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Guid queryId){
		throw new System.NotImplementedException();
	}
}
```
