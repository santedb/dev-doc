---
description: IJobManagerService (SanteDB.Core.Api)
---

## Summary
Job manager service

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Jobs|IEnumerable&lt;IJob>|R|Gets the status of all jobs|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AddJob|void|*IJob* **jobType**<br/>*TimeSpan* **elapseTime**<br/>*JobStartType* **startType**|Add a job|
|IsJobRegistered|Boolean|*Type* **jobType**|Returns true if the job is registered|
|StartJob|void|*IJob* **job**<br/>*Object[]* **parameters**|Start a job|
|GetJobInstance|IJob|*String* **jobTypeName**|Get this manager's instance of a job|

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
## Example Implementation
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
