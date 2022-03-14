`IThreadPoolService` in assembly SanteDB.Core.Api version 2.1.151.0

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
This class is a remnant / adaptation of the original thread pool service from OpenIZ because OpenIZ used PCL which
            didn't have a thread pool. Additionally it provided statistics on the thread pool load, etc. This has been
            refactored.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultThreadPoolService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Services.Impl.NetThreadPoolService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
