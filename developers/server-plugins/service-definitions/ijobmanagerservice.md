`IJobManagerService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Job manager service

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Jobs|IEnumerable&lt;IJob>|R|Gets the status of all jobs|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AddJob|void|*IJob* **jobType**<br/>*TimeSpan* **elapseTime**<br/>*JobStartType* **startType**|Add a job|
|AddJob|void|*IJob* **jobType**<br/>*JobStartType* **startType**|Add a job|
|IsJobRegistered|Boolean|*Type* **jobType**|Returns true if the job is registered|
|StartJob|void|*IJob* **job**<br/>*Object[]* **parameters**|Start a job|
|StartJob|void|*Type* **jobType**<br/>*Object[]* **parameters**|Start a job|
|GetJobInstance|IJob|*Guid* **jobKey**|Get this manager's instance of a job|
|GetJobSchedules|IEnumerable&lt;IJobSchedule>|*IJob* **job**|Get the schedule for the specified job|
|SetJobSchedule|IJobSchedule|*IJob* **job**<br/>*DayOfWeek[]* **daysOfWeek**<br/>*DateTime* **scheduleTime**|Schedule a job to start at a specific time|
|SetJobSchedule|IJobSchedule|*IJob* **job**<br/>*TimeSpan* **intervalSpan**|Schedule a job to start at a specific time|

# Implementations


## Default Job Manager - (SanteDB.Core.Api)
Represents the default implementation of the timer

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Jobs.DefaultJobManagerService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
	/// Add a job
	/// </summary>
	public void AddJob(IJob jobType,TimeSpan elapseTime,JobStartType startType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a job
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
	/// Start a job
	/// </summary>
	public void StartJob(IJob job,Object[] parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Start a job
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
	/// Get the schedule for the specified job
	/// </summary>
	public IEnumerable<IJobSchedule> GetJobSchedules(IJob job){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Schedule a job to start at a specific time
	/// </summary>
	public IJobSchedule SetJobSchedule(IJob job,DayOfWeek[] daysOfWeek,DateTime scheduleTime){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Schedule a job to start at a specific time
	/// </summary>
	public IJobSchedule SetJobSchedule(IJob job,TimeSpan intervalSpan){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJobManagerService.htm)
* [DefaultJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_DefaultJobManagerService.htm)
