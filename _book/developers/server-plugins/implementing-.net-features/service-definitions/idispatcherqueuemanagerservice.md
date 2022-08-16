`IDispatcherQueueManagerService` in assembly SanteDB.Core.Api version 2.1.151.0

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
		<add type="SanteDB.Core.Services.Impl.FileSystemDispatcherQueueService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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

### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		    <add type="SanteDB.Queue.RabbitMq.RabbitMqService, SanteDB.Queue.RabbitMq" />
		...
	</serviceProviders>
```

#### RabbitMQ Management API
To enable access to management API, first the RabbitMQ Management plugin must be enabled via the following command using the `rabbitmq-plugins` command line tool:
`rabbitmq-plugins enable rabbitmq_management`

For full instructions see  [RabbitMQ Management Plugin](https://www.rabbitmq.com/management.html). The RabbitMQ command line tools can be found under the `sbin` directory in RabbitMQ installation root. 

#### Configuration

|Configuration Attributes|Details| Default| 
|-|-|-|-|
| `hostname` | Name of the device hosting RabbitMQ. | **localhost** | 
| `virtualHost` | Segregates logical group of connections, exchanges, queues, bindings, user permissions, etc. within the same RabbitMQ instance.  | **/** | 
| `exchangeName` | Name of RabbitMQ exchange. |**SanteExc01** |
| `username` | Username to use when authenticating to the RabbitMQ server | **guest**| 
| `password` | Password to use when authenticating to the RabbitMQ server |**guest**|
| `durable` | This marks queues as durable, which means that it will survive a broker restart.  Please note that for messages (in queue) to survive broker restart, in addition to enabling this setting, published messages will have to be marked as persistent (see below). | **true** |
| `messagePersistence` | Determines whether messages will marked as persistent. For messages to survive broker restart, this must be enabled along with `durable` setting. | **true**|
| `lazy`  | Enabling this will allow queues to move their content to disk as early as practically possible, and only load the content in RAM when requested by consumers. |**true**|
| `maxUnackedMessageLimit` | Limits the number of unacknowledged messages on a channel to the number specified. Consumer will not receive any more messages once this number is reached until the the publisher starts receiving acknowledgement again.|**1**|
| `managementUri` | Sets the timeout duration in milliseconds when attempting to communicate with RabbitMQ management API. | **``http://localhost:15672/``**|
| `managementApiTimeout` | Sets the timeout duration in milliseconds when attempting to communicate with RabbitMQ management API. | **500**|


Example configuration section:
```markup
<section xsi:type="RabbitMqConfigurationSection" 
	hostname="localhost" 
	virtualHost="/" 
	exchangeName="SanteExc01" 
	username="guest" 
	password="guest" 
	durable="true"  
	messagePersistence="true" 
	lazy="true"  
	maxUnackedMessageLimit="1" 
	managementUri="http://localhost:15672/"
	managementApiTimeout="500"
/>
```

#### Users and Permissions
Additional users and permissions can be configured via management UI (see [RabbitMQ Management Plugin](https://www.rabbitmq.com/management.html)), or using the `rabbitmqctl` command line tool. For example, to create an user with username of `newadmin` & password of `secretpw`, you can use the following command:  
`rabbitmqctl add_user newadmin secretpw`

This user can be configured as administrator for full management UI and http API access, with this command:   
`rabbitmqctl set_user_tags newadmin administrator`

For more fine-grained control of user and permissions, view RabbitMQ documentation here - [Authentication, Authorisation, Access Control](https://www.rabbitmq.com/access-control.html)).

#### What to expect
On successful configuration and after enabling the RabbitMQ Management plugin, you will be able to access the management UI by navigating to the management Uri and logging in with admin credentials. Once logged in, the plugin functionality can be validated the following:

1. Exchange was created by navigating to `Exchanges` tabs, and confirming that appropriate exchange with the name specified in configuration exists:

![](<../../../../../../../_book/.gitbook/assets/rabbitmq_exchange_tab.png>)

2. Appropriate queues were created by navigating to `Queues` tab:

![](<../../../../../../../_book/.gitbook/assets/rabbitmq_queues_tab.png>)

3. If any messages were enqueued and dequeued on any created queue, you will be able to view the activity under message rates by selecting the queue from the `Queues` tab.

![](<../../../../../../../_book/.gitbook/assets/rabbitmq_queue_activity.png>)

## FileSystemQueueService - (SanteDB.Server.Core)
Represents a file system queue that monitors directories

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.FileSystemQueueService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
* [FileSystemDispatcherQueueService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_FileSystemDispatcherQueueService.htm)
* [MsmqPersistentQueueService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Queue_Msmq_MsmqPersistentQueueService.htm)
* [FileSystemQueueService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_FileSystemQueueService.htm)
