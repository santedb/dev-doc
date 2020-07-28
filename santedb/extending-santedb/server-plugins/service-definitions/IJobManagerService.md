---
description: IJobManagerService (SanteDB.Core.Api)
---

## Summary
Job manager service

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
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Jobs.IJob> Jobs {
		get;
	}
	/// <summary>
	/// Add a job
	/// </summary>
	public void AddJob(SanteDB.Core.Jobs.IJob jobType,System.TimeSpan elapseTime,SanteDB.Core.Jobs.JobStartType startType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the job is registered
	/// </summary>
	public System.Boolean IsJobRegistered(System.Type jobType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Start a job
	/// </summary>
	public void StartJob(SanteDB.Core.Jobs.IJob job,System.Object[] parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get this manager's instance of a job
	/// </summary>
	public SanteDB.Core.Jobs.IJob GetJobInstance(System.String jobTypeName){
		throw new System.NotImplementedException();
	}
}
```
