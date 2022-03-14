`ISubscriptionExecutor` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Contract which defines a dCDR subscription executor

## Description
The subscription executor is responsible for the translation of a dCDR [SubscriptionDefinition](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Subscription_SubscriptionDefinition.htm)
            from the [ISubscriptionRepository](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionRepository.htm) to the appropriate database technology. The subscription executor
            gathers any new records requested by the dCDR and prepares them for download by the dCDR.

# Events

|Event|Type|Description|
|-|-|-|
|Executed|EventHandler&lt;QueryResultEventArgs&lt;IdentifiedData>>|Occurs after a subscription has been executed, and allows subscribers to modify the data being            sent back to the dCDR|
|Executing|EventHandler&lt;QueryRequestEventArgs&lt;IdentifiedData>>|Occurs prior to a subscription being executed, and allows subscribers to modify the query being            executed.|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Execute|IEnumerable&lt;Object>|*Guid* **subscriptionKey**<br/>*NameValueCollection* **parameters**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**|Executes the identified subscription agianst the persistence layer.|
|Execute|IEnumerable&lt;Object>|*SubscriptionDefinition* **subscription**<br/>*NameValueCollection* **parameters**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**|Executes the identified subscription agianst the persistence layer.|

# Implementations


## ADO.NET Subscription Executor - (SanteDB.Persistence.Data.ADO)
An implementation of the [ISubscriptionExecutor](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionExecutor.htm) which uses an ADO persistence layer

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
	/// Occurs after a subscription has been executed, and allows subscribers to modify the data being            sent back to the dCDR
	/// </summary>
	public event EventHandler<QueryResultEventArgs<IdentifiedData>> Executed;
	/// <summary>
	/// Occurs prior to a subscription being executed, and allows subscribers to modify the query being            executed.
	/// </summary>
	public event EventHandler<QueryRequestEventArgs<IdentifiedData>> Executing;
	/// <summary>
	/// Executes the identified subscription agianst the persistence layer.
	/// </summary>
	public IEnumerable<Object> Execute(Guid subscriptionKey,NameValueCollection parameters,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Executes the identified subscription agianst the persistence layer.
	/// </summary>
	public IEnumerable<Object> Execute(SubscriptionDefinition subscription,NameValueCollection parameters,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISubscriptionExecutor C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionExecutor.htm)
* [AdoSubscriptionExecutor C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoSubscriptionExecutor.htm)
