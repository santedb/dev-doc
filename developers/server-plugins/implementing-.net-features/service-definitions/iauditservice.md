`IAuditService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Auditing Service for SanteDB. [IAuditService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IAuditService.htm) replaces the obsolete [AuditUtil](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Audit_AuditUtil.htm) static implementation.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Audit|IAuditBuilder|*none*|TODO|
|SendAudit|void|*AuditEventData* **audit**|Sends an audit event to be processed.|
|DispatchAudit|void|*AuditEventData* **audit**|Directly dispatches the audit to a local repository or an audit dispatcher.|

# Implementations


## Default Audit Service - (SanteDB.Core.Api)
The default implementation of the audit service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.Audit.DefaultAuditService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyAuditService : SanteDB.Core.Security.Services.IAuditService { 
	public String ServiceName => "My own IAuditService service";
	public IAuditBuilder Audit(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Sends an audit event to be processed.
	/// </summary>
	public void SendAudit(AuditEventData audit){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Directly dispatches the audit to a local repository or an audit dispatcher.
	/// </summary>
	public void DispatchAudit(AuditEventData audit){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IAuditService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IAuditService.htm)
* [DefaultAuditService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Audit_DefaultAuditService.htm)
