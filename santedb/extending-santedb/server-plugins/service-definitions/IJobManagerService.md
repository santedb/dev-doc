---
description: IJobManagerService (SanteDB.Core.Api)
---

## Summary
Job manager service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Jobs|IEnumerable&lt;IJob>|R|Gets the status of all jobs|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AddJob|void|jobType <small style='border:solid 1px #aaa'>IJob</small><br/>elapseTime <small style='border:solid 1px #aaa'>TimeSpan</small><br/>startType <small style='border:solid 1px #aaa'>JobStartType</small>|Add a job|
|IsJobRegistered|Boolean|jobType <small style='border:solid 1px #aaa'>Type</small>|Returns true if the job is registered|
|StartJob|void|job <small style='border:solid 1px #aaa'>IJob</small><br/>parameters <small style='border:solid 1px #aaa'>Object[]</small>|Start a job|
|GetJobInstance|IJob|jobTypeName <small style='border:solid 1px #aaa'>String</small>|Get this manager's instance of a job|

## Implementations


### Default Job Manager - (SanteDB.Core)
Represents the default implementation of the timer

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.DefaultJobManagerService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Jobs;
/// Other usings here
public class MyJobManagerService : SanteDB.Core.Jobs.IJobManagerService { 
	public String ServiceName => "My own IJobManagerService service";
	/// <summary>
	/// Gets the status of all jobs
	/// </summary>
	public IEnumerable<IJob> Jobs {
		get;
	}
	/// <summary>
	/// Add a job
	/// </summary>
	public void AddJob(IJob jobType,TimeSpan elapseTime,JobStartType startType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the job is registered
	/// </summary>
	public Boolean IsJobRegistered(Type jobType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Start a job
	/// </summary>
	public void StartJob(IJob job,Object[] parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get this manager's instance of a job
	/// </summary>
	public IJob GetJobInstance(String jobTypeName){
		throw new System.NotImplementedException();
	}
}
```
