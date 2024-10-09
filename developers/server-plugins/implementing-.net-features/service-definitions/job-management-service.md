`IJobManagerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Job Management Service

## Description
In SanteDB, developers can create [IJob](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJob.htm) implementations which represent background jobs for the system. Uses of these classes involve:

* Performing routine maintenance tasks like compression, backup, etc.
* Performing indexing tasks or managing long-running tasks
* Exposing packaged batch operations to users (who can run them manually from the UI)


The job manager is the service which manages the master list of [IJob](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJob.htm) instances and allows other plugins
            to register new jobs, start jobs, and even schedule job execution based on a schedule or interval.

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Jobs|IEnumerable&lt;IJob>|R|Gets the status of all jobs|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AddJob|void|*IJob* **jobType**<br/>*TimeSpan* **elapseTime**<br/>*JobStartType* **startType**|Add a job to the job manager|
|RegisterJob|IJob|*Type* **jobType**|Adds a job by type to the job manager|
|AddJob|void|*IJob* **jobType**<br/>*JobStartType* **startType**|Add a job to the job manager|
|IsJobRegistered|Boolean|*Type* **jobType**|Returns true if the job is registered|
|StartJob|void|*IJob* **job**<br/>*Object[]* **parameters**|Starts the specified|
|StartJob|void|*Type* **jobType**<br/>*Object[]* **parameters**|Starts the specified|
|GetJobInstance|IJob|*Guid* **jobKey**|Get this manager's instance of a job|
|GetJobInstance|IJob|*Type* **jobType**|Get this manager's instance of a job|
|GetJobSchedules|IEnumerable&lt;IJobSchedule>|*IJob* **job**|Get the schedule for the specified job|
|SetJobSchedule|IJobSchedule|*IJob* **job**<br/>*DayOfWeek[]* **daysOfWeek**<br/>*DateTime* **scheduleTime**|Schedule a job to start at a specific time with a specific repetition|
|SetJobSchedule|IJobSchedule|*IJob* **job**<br/>*TimeSpan* **intervalSpan**|Schedule a job to start at a specific time with a specific repetition|
|ClearJobSchedule|void|*IJob* **job**|Clear the schedule of a job.|
|GetAvailableJobs|IEnumerable&lt;Type>|*none*|TODO|

# Implementations


## UpstreamJobManager - (SanteDB.Client)
Represents a [IJobManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJobManagerService.htm) which operates only on the upstream jobs service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Management.UpstreamJobManager, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Default Job Manager - (SanteDB.Core.Api)
SanteDB's default implementation of the [IJobManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJobManagerService.htm)
### Description


### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Jobs.DefaultJobManagerService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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
	/// Add a job to the job manager
	/// </summary>
	public void AddJob(IJob jobType,TimeSpan elapseTime,JobStartType startType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds a job by type to the job manager
	/// </summary>
	public IJob RegisterJob(Type jobType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a job to the job manager
	/// </summary>
	public void AddJob(IJob jobType,JobStartType startType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the job is registered
	/// </summary>
	public Boolean IsJobRegistered(Type jobType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Starts the specified
	/// </summary>
	public void StartJob(IJob job,Object[] parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Starts the specified
	/// </summary>
	public void StartJob(Type jobType,Object[] parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get this manager's instance of a job
	/// </summary>
	public IJob GetJobInstance(Guid jobKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get this manager's instance of a job
	/// </summary>
	public IJob GetJobInstance(Type jobType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the schedule for the specified job
	/// </summary>
	public IEnumerable<IJobSchedule> GetJobSchedules(IJob job){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Schedule a job to start at a specific time with a specific repetition
	/// </summary>
	public IJobSchedule SetJobSchedule(IJob job,DayOfWeek[] daysOfWeek,DateTime scheduleTime){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Schedule a job to start at a specific time with a specific repetition
	/// </summary>
	public IJobSchedule SetJobSchedule(IJob job,TimeSpan intervalSpan){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clear the schedule of a job.
	/// </summary>
	public void ClearJobSchedule(IJob job){
		throw new System.NotImplementedException();
	}
	public IEnumerable<Type> GetAvailableJobs(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJobManagerService.htm)
* [UpstreamJobManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Management_UpstreamJobManager.htm)
* [DefaultJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_DefaultJobManagerService.htm)
