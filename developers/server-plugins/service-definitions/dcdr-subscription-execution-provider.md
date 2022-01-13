---
description: dCDR Subscription Execution Provider (ISubscriptionExecutor in SanteDB.Core.Api)
---

# Summary
Represents a subscription executor

# Events

|Event|Type|Description|
|-|-|-|
|Executed|EventHandler&lt;QueryResultEventArgs&lt;IdentifiedData>>|Occurs when queried.|
|Executing|EventHandler&lt;QueryRequestEventArgs&lt;IdentifiedData>>|Occurs when querying.|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Execute|IEnumerable&lt;Object>|*Guid* **subscriptionKey**<br/>*NameValueCollection* **parameters**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**|Executes the specified subscription mechanism|
|Execute|IEnumerable&lt;Object>|*SubscriptionDefinition* **subscription**<br/>*NameValueCollection* **parameters**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**|Executes the specified subscription mechanism|

# Implementations


## ADO.NET Subscription Executor - (SanteDB.Persistence.Data.ADO)
Represents a default implementation of the subscription executor

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSubscriptionExecutor, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySubscriptionExecutor : SanteDB.Core.Services.ISubscriptionExecutor { 
	public String ServiceName => "My own ISubscriptionExecutor service";
	/// <summary>
	/// Occurs when queried.
	/// </summary>
	public event EventHandler<QueryResultEventArgs<IdentifiedData>> Executed;
	/// <summary>
	/// Occurs when querying.
	/// </summary>
	public event EventHandler<QueryRequestEventArgs<IdentifiedData>> Executing;
	/// <summary>
	/// Executes the specified subscription mechanism
	/// </summary>
	public IEnumerable<Object> Execute(Guid subscriptionKey,NameValueCollection parameters,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the specified subscription mechanism
	/// </summary>
	public IEnumerable<Object> Execute(SubscriptionDefinition subscription,NameValueCollection parameters,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISubscriptionExecutor C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionExecutor.htm)
* [AdoSubscriptionExecutor C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoSubscriptionExecutor.htm)
