---
description: IThreadPoolService (SanteDB.Core.Api)
---

## Summary
Represents a thread pooling service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|QueueUserWorkItem|void|action <small style='border:solid 1px #aaa'>System.Action<System.Object></small>|Queues the specified action into the worker pool|
|QueueUserWorkItem|void|action <small style='border:solid 1px #aaa'>System.Action<System.Object></small><br/>parm <small style='border:solid 1px #aaa'>System.Object</small>|Queues the specified action into the worker pool|
|QueueUserWorkItem|void|timeout <small style='border:solid 1px #aaa'>System.TimeSpan</small><br/>action <small style='border:solid 1px #aaa'>System.Action<System.Object></small><br/>parm <small style='border:solid 1px #aaa'>System.Object</small>|Queues the specified action into the worker pool|
|QueueNonPooledWorkItem|void|action <small style='border:solid 1px #aaa'>System.Action<System.Object></small><br/>parm <small style='border:solid 1px #aaa'>System.Object</small>|Creates a normal thread which is not in the pool|

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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyThreadPoolService : SanteDB.Core.Services.IThreadPoolService { 
	public String ServiceName => "My own IThreadPoolService service";
	/// <summary>
	/// Queues the specified action into the worker pool
	/// </summary>
	public void QueueUserWorkItem(System.Action<System.Object> action){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Queues the specified action into the worker pool
	/// </summary>
	public void QueueUserWorkItem(System.Action<System.Object> action,System.Object parm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Queues the specified action into the worker pool
	/// </summary>
	public void QueueUserWorkItem(System.TimeSpan timeout,System.Action<System.Object> action,System.Object parm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Creates a normal thread which is not in the pool
	/// </summary>
	public void QueueNonPooledWorkItem(System.Action<System.Object> action,System.Object parm){
		throw new System.NotImplementedException();
	}
}
```
