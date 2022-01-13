`IPubSubManagerService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a pub/sub manager service

# Events

|Event|Type|Description|
|-|-|-|
|Subscribing|EventHandler&lt;DataPersistingEventArgs&lt;PubSubSubscriptionDefinition>>|Fired when a subscription is requested, but not yet registered|
|Subscribed|EventHandler&lt;DataPersistedEventArgs&lt;PubSubSubscriptionDefinition>>|Fired after a subscription has been registered|
|UnSubscribing|EventHandler&lt;DataPersistingEventArgs&lt;PubSubSubscriptionDefinition>>|Fired when an unsubscription is requested|
|UnSubscribed|EventHandler&lt;DataPersistedEventArgs&lt;PubSubSubscriptionDefinition>>|Fired when a subscription has been terminated|
|Activating|EventHandler&lt;DataPersistingEventArgs&lt;PubSubSubscriptionDefinition>>|Fired after a subscription and channel are activating|
|DeActivating|EventHandler&lt;DataPersistingEventArgs&lt;PubSubSubscriptionDefinition>>|Fired after a subscription and channel are deactivating|
|Activated|EventHandler&lt;DataPersistedEventArgs&lt;PubSubSubscriptionDefinition>>|Fired after a subscription and channel are activated|
|DeActivated|EventHandler&lt;DataPersistedEventArgs&lt;PubSubSubscriptionDefinition>>|Fired after a subscription and channel are deactivated|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindChannel|IEnumerable&lt;PubSubChannelDefinition>|*Expression&lt;Func&lt;PubSubChannelDefinition,Boolean>>* **filter**|Find an existing channel|
|FindSubscription|IEnumerable&lt;PubSubSubscriptionDefinition>|*Expression&lt;Func&lt;PubSubSubscriptionDefinition,Boolean>>* **filter**|Find an existing subscription|
|FindChannel|IEnumerable&lt;PubSubChannelDefinition>|*Expression&lt;Func&lt;PubSubChannelDefinition,Boolean>>* **filter**<br/>*Int32* **offset**<br/>*Int32* **count**<br/>*Int32&* **totalResults**|Find an existing channel|
|FindSubscription|IEnumerable&lt;PubSubSubscriptionDefinition>|*Expression&lt;Func&lt;PubSubSubscriptionDefinition,Boolean>>* **filter**<br/>*Int32* **offset**<br/>*Int32* **count**<br/>*Int32&* **totalResults**|Find an existing subscription|
|RegisterChannel|PubSubChannelDefinition|*String* **name**<br/>*Type* **dispatcherFactoryType**<br/>*Uri* **endpoint**<br/>*IDictionary&lt;String,String>* **settings**|Registers the specified pub-sub channel using the specified dispatcher|
|RegisterChannel|PubSubChannelDefinition|*String* **name**<br/>*String* **dispatchFactoryId**<br/>*Uri* **endpoint**<br/>*IDictionary&lt;String,String>* **settings**|Registers the specified pub-sub channel using the specified dispatcher|
|UpdateChannel|PubSubChannelDefinition|*Guid* **key**<br/>*String* **name**<br/>*Uri* **endpoint**<br/>*IDictionary&lt;String,String>* **settings**|Updates the specified pub-sub channel|
|RegisterSubscription|PubSubSubscriptionDefinition|*String* **name**<br/>*String* **description**<br/>*PubSubEventType* **events**<br/>*Expression&lt;Func&lt;TModel,Boolean>>* **filter**<br/>*Guid* **channelId**<br/>*String* **supportAddress**<br/>*Nullable&lt;DateTimeOffset>* **notBefore**<br/>*Nullable&lt;DateTimeOffset>* **notAfter**|Register a new subscription for the specified type|
|RegisterSubscription|PubSubSubscriptionDefinition|*Type* **modelType**<br/>*String* **name**<br/>*String* **description**<br/>*PubSubEventType* **events**<br/>*String* **hdsiFilter**<br/>*Guid* **channelId**<br/>*String* **supportAddress**<br/>*Nullable&lt;DateTimeOffset>* **notBefore**<br/>*Nullable&lt;DateTimeOffset>* **notAfter**|Register a new subscription for the specified type|
|UpdateSubscription|PubSubSubscriptionDefinition|*Guid* **key**<br/>*String* **name**<br/>*String* **description**<br/>*PubSubEventType* **events**<br/>*String* **hdsiFilter**<br/>*String* **supportAddress**<br/>*Nullable&lt;DateTimeOffset>* **notBefore**<br/>*Nullable&lt;DateTimeOffset>* **notAfter**|Update subscription data|
|ActivateSubscription|PubSubSubscriptionDefinition|*Guid* **key**<br/>*Boolean* **isActive**|Activate a subscription|
|GetSubscription|PubSubSubscriptionDefinition|*Guid* **id**|Gets the subscription information|
|GetChannel|PubSubChannelDefinition|*Guid* **id**|Gets the channel information|
|RemoveChannel|PubSubChannelDefinition|*Guid* **id**|Removes the specified channel and all related subscriptions|
|RemoveSubscription|PubSubSubscriptionDefinition|*Guid* **id**|Removes the subscription|
|GetSubscriptionByName|PubSubSubscriptionDefinition|*String* **name**|Get subscription by its name|

# Implementations


## ADO.NET Pub/Sub Subscription Manager - (SanteDB.Persistence.PubSub.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.PubSub.ADO.AdoPubSubManager, SanteDB.Persistence.PubSub.ADO, Version=2.1.3.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.PubSub;
/// Other usings here
public class MyPubSubManagerService : SanteDB.Core.PubSub.IPubSubManagerService { 
	public String ServiceName => "My own IPubSubManagerService service";
	/// <summary>
	/// Fired when a subscription is requested, but not yet registered
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<PubSubSubscriptionDefinition>> Subscribing;
	/// <summary>
	/// Fired after a subscription has been registered
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<PubSubSubscriptionDefinition>> Subscribed;
	/// <summary>
	/// Fired when an unsubscription is requested
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<PubSubSubscriptionDefinition>> UnSubscribing;
	/// <summary>
	/// Fired when a subscription has been terminated
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<PubSubSubscriptionDefinition>> UnSubscribed;
	/// <summary>
	/// Fired after a subscription and channel are activating
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<PubSubSubscriptionDefinition>> Activating;
	/// <summary>
	/// Fired after a subscription and channel are deactivating
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<PubSubSubscriptionDefinition>> DeActivating;
	/// <summary>
	/// Fired after a subscription and channel are activated
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<PubSubSubscriptionDefinition>> Activated;
	/// <summary>
	/// Fired after a subscription and channel are deactivated
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<PubSubSubscriptionDefinition>> DeActivated;
	/// <summary>
	/// Find an existing channel
	/// </summary>
	public IEnumerable<PubSubChannelDefinition> FindChannel(Expression<Func<PubSubChannelDefinition,Boolean>> filter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an existing subscription
	/// </summary>
	public IEnumerable<PubSubSubscriptionDefinition> FindSubscription(Expression<Func<PubSubSubscriptionDefinition,Boolean>> filter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an existing channel
	/// </summary>
	public IEnumerable<PubSubChannelDefinition> FindChannel(Expression<Func<PubSubChannelDefinition,Boolean>> filter,Int32 offset,Int32 count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find an existing subscription
	/// </summary>
	public IEnumerable<PubSubSubscriptionDefinition> FindSubscription(Expression<Func<PubSubSubscriptionDefinition,Boolean>> filter,Int32 offset,Int32 count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Registers the specified pub-sub channel using the specified dispatcher
	/// </summary>
	public PubSubChannelDefinition RegisterChannel(String name,Type dispatcherFactoryType,Uri endpoint,IDictionary<String,String> settings){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Registers the specified pub-sub channel using the specified dispatcher
	/// </summary>
	public PubSubChannelDefinition RegisterChannel(String name,String dispatchFactoryId,Uri endpoint,IDictionary<String,String> settings){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Updates the specified pub-sub channel
	/// </summary>
	public PubSubChannelDefinition UpdateChannel(Guid key,String name,Uri endpoint,IDictionary<String,String> settings){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Register a new subscription for the specified type
	/// </summary>
	public PubSubSubscriptionDefinition RegisterSubscription<TModel>(String name,String description,PubSubEventType events,Expression<Func<TModel,Boolean>> filter,Guid channelId,String supportAddress,Nullable<DateTimeOffset> notBefore,Nullable<DateTimeOffset> notAfter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Register a new subscription for the specified type
	/// </summary>
	public PubSubSubscriptionDefinition RegisterSubscription(Type modelType,String name,String description,PubSubEventType events,String hdsiFilter,Guid channelId,String supportAddress,Nullable<DateTimeOffset> notBefore,Nullable<DateTimeOffset> notAfter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Update subscription data
	/// </summary>
	public PubSubSubscriptionDefinition UpdateSubscription(Guid key,String name,String description,PubSubEventType events,String hdsiFilter,String supportAddress,Nullable<DateTimeOffset> notBefore,Nullable<DateTimeOffset> notAfter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Activate a subscription
	/// </summary>
	public PubSubSubscriptionDefinition ActivateSubscription(Guid key,Boolean isActive){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the subscription information
	/// </summary>
	public PubSubSubscriptionDefinition GetSubscription(Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the channel information
	/// </summary>
	public PubSubChannelDefinition GetChannel(Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the specified channel and all related subscriptions
	/// </summary>
	public PubSubChannelDefinition RemoveChannel(Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the subscription
	/// </summary>
	public PubSubSubscriptionDefinition RemoveSubscription(Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get subscription by its name
	/// </summary>
	public PubSubSubscriptionDefinition GetSubscriptionByName(String name){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPubSubManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_IPubSubManagerService.htm)
* [AdoPubSubManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_PubSub_ADO_AdoPubSubManager.htm)
