`IDispatcherQueueManagerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
A service which is responsible for storing messages in a reliable place for dispatching

## Description
Whenever SanteDB sends messages to another system using messaging, there is no guarantee that the remote endpoint will be available,
            or accessable, etc. Therefore all messages which are sent (dispatched) to a remote system are first queued using this wrapper service.
            
The purpose of the dispatcher queue is the store the outbound message locally in some persistent place, then to notify any
            listeners that a new message is ready for sending. If the message cannot be sent, then the sending service should place
            the message back onto the queue or onto a dedicated deadletter queue.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Open|void|*String* **queueName**|Opens the specified queue name and enables subscriptions|
|SubscribeTo|void|*String* **queueName**<br/>*DispatcherQueueCallback* **callback**|Subscribes to  using|
|UnSubscribe|void|*String* **queueName**<br/>*DispatcherQueueCallback* **callback**|Remove the callback registration|
|Enqueue|void|*String* **queueName**<br/>*Object* **data**|Enqueue the specified data to the persistent queue|
|Dequeue|DispatcherQueueEntry|*String* **queueName**|Dequeues the last added item from the persistent queue|
|DequeueById|DispatcherQueueEntry|*String* **queueName**<br/>*String* **correlationId**|De-queue a specific message|
|Purge|void|*String* **queueName**|Purge the queue|
|Move|DispatcherQueueEntry|*DispatcherQueueEntry* **entry**<br/>*String* **toQueue**|Move an entry from one queue to another|
|GetQueueEntry|DispatcherQueueEntry|*String* **queueName**<br/>*String* **correlationId**|Get the specified queue entry|
|GetQueues|IEnumerable&lt;DispatcherQueueInfo>|*none*|TODO|
|GetQueueEntries|IEnumerable&lt;DispatcherQueueEntry>|*String* **queueName**|Get all queue entries|

# Implementations


## FileSystemDispatcherQueueService - (SanteDB.Core.Api)
A persistent queue service that uses the file system (use when there's no other infrastructure)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.FileSystemDispatcherQueueService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MsmqPersistentQueueService - (SanteDB.Queue.Msmq)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Queue.Msmq.MsmqPersistentQueueService, SanteDB.Queue.Msmq, Version=2.1.132.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## RabbitMqService - (SanteDB.Queue.RabbitMq)
An implementation of the [IDispatcherQueueManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Queue_IDispatcherQueueManagerService.htm) which uses RabbitMQ as the queue managing service
### Description
This queue service uses RabbitMQ to manage queues and loading/unloading of items to queues.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Queue.RabbitMq.RabbitMqService, SanteDB.Queue.RabbitMq, Version=2.1.132.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Queue;
/// Other usings here
public class MyDispatcherQueueManagerService : SanteDB.Core.Queue.IDispatcherQueueManagerService { 
	public String ServiceName => "My own IDispatcherQueueManagerService service";
	/// <summary>
	/// Opens the specified queue name and enables subscriptions
	/// </summary>
	public void Open(String queueName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Subscribes to  using
	/// </summary>
	public void SubscribeTo(String queueName,DispatcherQueueCallback callback){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove the callback registration
	/// </summary>
	public void UnSubscribe(String queueName,DispatcherQueueCallback callback){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Enqueue the specified data to the persistent queue
	/// </summary>
	public void Enqueue(String queueName,Object data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Dequeues the last added item from the persistent queue
	/// </summary>
	public DispatcherQueueEntry Dequeue(String queueName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// De-queue a specific message
	/// </summary>
	public DispatcherQueueEntry DequeueById(String queueName,String correlationId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Purge the queue
	/// </summary>
	public void Purge(String queueName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Move an entry from one queue to another
	/// </summary>
	public DispatcherQueueEntry Move(DispatcherQueueEntry entry,String toQueue){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified queue entry
	/// </summary>
	public DispatcherQueueEntry GetQueueEntry(String queueName,String correlationId){
		throw new System.NotImplementedException();
	}
	public IEnumerable<DispatcherQueueInfo> GetQueues(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all queue entries
	/// </summary>
	public IEnumerable<DispatcherQueueEntry> GetQueueEntries(String queueName){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDispatcherQueueManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Queue_IDispatcherQueueManagerService.htm)
* [Persistent queue service using a file system directory for storage C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_FileSystemDispatcherQueueService.htm)
* [MsmqPersistentQueueService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Queue_Msmq_MsmqPersistentQueueService.htm)
* [RabbitMqService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Queue_RabbitMq_RabbitMqService.htm)
