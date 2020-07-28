---
description: IThreadPoolService (SanteDB.Core.Api)
---

## Summary
Represents a thread pooling service

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|QueueUserWorkItem|void|*Action&lt;Object>* **action**|Queues the specified action into the worker pool|
|QueueUserWorkItem|void|*Action&lt;Object>* **action**<br/>*Object* **parm**|Queues the specified action into the worker pool|
|QueueUserWorkItem|void|*TimeSpan* **timeout**<br/>*Action&lt;Object>* **action**<br/>*Object* **parm**|Queues the specified action into the worker pool|
|QueueNonPooledWorkItem|void|*Action&lt;Object>* **action**<br/>*Object* **parm**|Creates a normal thread which is not in the pool|

## Implementations


### DefaultThreadPoolService - (SanteDB.Core.Api)
Represents a thread pool which is implemented separately from the default .net
            threadpool, this is to reduce the load on the .net framework thread pool

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultThreadPoolService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
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
	/// Queues the specified action into the worker pool
	/// </summary>
	public void QueueUserWorkItem(Action<Object> action,Object parm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Queues the specified action into the worker pool
	/// </summary>
	public void QueueUserWorkItem(TimeSpan timeout,Action<Object> action,Object parm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Creates a normal thread which is not in the pool
	/// </summary>
	public void QueueNonPooledWorkItem(Action<Object> action,Object parm){
		throw new System.NotImplementedException();
	}
}
```
