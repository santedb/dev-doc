`IThreadPoolService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a thread pooling service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|QueueUserWorkItem|void|*Action&lt;Object>* **action**|Queues the specified action into the worker pool|
|QueueUserWorkItem|void|*Action&lt;TParam>* **action**<br/>*TParam* **parm**|Queue user work item|
|GetWorkerStatus|void|*Int32&* **totalWorkers**<br/>*Int32&* **availableWorkers**<br/>*Int32&* **waitingInQueue**|Get worker status|

# Implementations


## DefaultThreadPoolService - (SanteDB.Core.Api)
Represents a thread pool which is implemented separately from the default .net
            threadpool, this is to reduce the load on the .net framework thread pool
### Description
Many SanteDB jobs use threads to perform background tasks such as refreshes, matching,
            job execution, etc. Because we don't want uncontrolled explosion of threads, we use a thread pool 
            in order to control the number of active threads which are being used.
            


            Implementers may choose to register a [IThreadPoolService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IThreadPoolService.htm) which uses the .NET [ThreadPool](https://docs.microsoft.com/en-us/dotnet/api/system.threading.threadpool) (see: [NetThreadPoolService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_NetThreadPoolService.htm)), 
            or they can choose to use this separate thread pool service. There are several advantages to using the SanteDB thread pool rather than the 
            .NET thread pool including:
            

* The default .NET thread pool can bounce work between threads when the thread enters a wait state, this can cause issues with the REDIS connection multiplexer
* SanteDB plugins may use PLINQ or other TPL libraries which require using .NET thread pool - and we don't want longer running processess consuming those threads
* Implementers may wish to have more control over how the Thread pool uses resources


This thread pool works by spinning up a pool of threads which wait for [Object})](#Object})) which initiates (or queues) a request to 
            perform background work. When an available thread in the pool can execute the task, the task will be run and the thread will work on the next work item.

If the thread pool needs additional threads (i.e. there are a lot of items in the backlog) it will spin up new reserved threads at a rate of 
            number of CPUs on the machine. This continues until the environment variable SDB_MAX_THREADS_PER_CPU is hit.

Conversely, if the thread pool threads remain idle for too long (1 minute) they are destroyed and removed from the thread pool. This ensures over-threading
            is not done on the host machine.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultThreadPoolService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## NetThreadPoolService - (SanteDB.Core.Api)
Represents a thread pool which is implemented to wrap .NET thread pool
### Description
This class is a remnant / adaptation of the original thread pool service from OpenIZ because OpenIZ used PCL which
            didn't have a thread pool. Additionally it provided statistics on the thread pool load, etc. This has been
            refactored.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.NetThreadPoolService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyThreadPoolService : SanteDB.Core.Services.IThreadPoolService { 
	public String ServiceName => "My own IThreadPoolService service";
	/// <summary>
	/// Queues the specified action into the worker pool
	/// </summary>
	public void QueueUserWorkItem(Action<Object> action){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Queue user work item
	/// </summary>
	public void QueueUserWorkItem<TParam>(Action<TParam> action,TParam parm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get worker status
	/// </summary>
	public void GetWorkerStatus(Int32& totalWorkers,Int32& availableWorkers,Int32& waitingInQueue){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IThreadPoolService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IThreadPoolService.htm)
* [DefaultThreadPoolService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_DefaultThreadPoolService.htm)
* [NetThreadPoolService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_NetThreadPoolService.htm)
