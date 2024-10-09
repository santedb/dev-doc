`ILogManagerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which can be used to manage the log files for the application instance

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetLogFiles|IEnumerable&lt;FileInfo>|*none*|TODO|
|GetLogFile|FileInfo|*String* **logId**|Get the log file given the specified log identifier|
|DeleteLogFile|void|*String* **logId**|Delete or remove a log file from the infrastructure|

# Implementations


## RolloverLogManagerService - (SanteDB.Core.Api)
A log file manager service which manages rollover logs

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Diagnostics.Tracing.RolloverLogManagerService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Diagnostics;
/// Other usings here
public class MyLogManagerService : SanteDB.Core.Diagnostics.ILogManagerService { 
	public String ServiceName => "My own ILogManagerService service";
	public IEnumerable<FileInfo> GetLogFiles(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the log file given the specified log identifier
	/// </summary>
	public FileInfo GetLogFile(String logId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete or remove a log file from the infrastructure
	/// </summary>
	public void DeleteLogFile(String logId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ILogManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Diagnostics_ILogManagerService.htm)
* [RolloverLogManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Diagnostics_Tracing_RolloverLogManagerService.htm)
