`IAuditDaemon` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which starts up and binds itself to key system events

# Implementations


## Security Audit Service - (SanteDB.Core.Api)
An implementation of [IDaemonService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm) which monitors instances of [IIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IIdentityProviderService.htm)
            and [ISessionIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionIdentityProviderService.htm) to audit login and logout events in the audit repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.Audit.AuditDaemonService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Audit;
/// Other usings here
public class MyAuditDaemon : SanteDB.Core.Security.Audit.IAuditDaemon { 
	public String ServiceName => "My own IAuditDaemon service";
}
```

# References

* [IAuditDaemon C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Audit_IAuditDaemon.htm)
* [AuditDaemonService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Audit_AuditDaemonService.htm)
