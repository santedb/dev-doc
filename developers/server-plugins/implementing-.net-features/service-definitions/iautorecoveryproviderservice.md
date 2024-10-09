`IAutoRecoveryProviderService` in assembly SanteDB.Client version 3.0.1980.0

# Summary
Represents a service that can provide auto-recovery services

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetRecoveryPoints|IEnumerable&lt;DateTime>|*none*|TODO|
|RestoreRecoveryPoint|void|*DateTime* **recoveryDate**|Restores the recovery point|
|CreateRecoveryPoint|void|*none*|TODO|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Client.Services;
/// Other usings here
public class MyAutoRecoveryProviderService : SanteDB.Client.Services.IAutoRecoveryProviderService { 
	public String ServiceName => "My own IAutoRecoveryProviderService service";
	public IEnumerable<DateTime> GetRecoveryPoints(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Restores the recovery point
	/// </summary>
	public void RestoreRecoveryPoint(DateTime recoveryDate){
		throw new System.NotImplementedException();
	}
	public void CreateRecoveryPoint(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IAutoRecoveryProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Services_IAutoRecoveryProviderService.htm)
