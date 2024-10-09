`IRequestRestarts` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
A service implementation that can request restarts of the application context
            (configuration changes, backups, etc.)

# Events

|Event|Type|Description|
|-|-|-|
|RestartRequested|EventHandler|Fired when the backup service requires a restart|

# Implementations


## InitialConfigurationManager - (SanteDB.Client)
A configuration manager which uses a temporary configuration in memory 
            via implementations of [IInitialConfigurationProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Configuration_IInitialConfigurationProvider.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Configuration.InitialConfigurationManager, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local File Configuration Manager - (SanteDB.Core.Api)
Provides a redirected configuration service which reads configuration information from a file
### Description
This configuration manager implementation  reads from the configuration file ```santedb.config.xml``` in the same directory
            as the installed iCDR instance. This file is create either manually ([as documented here](https://help.santesuite.org/operations/server-administration/host-configuration-file)), or
            using the [Configuration Tool](https://help.santesuite.org/operations/server-administration/configuration-tool).

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.FileConfigurationService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DefaultBackupManager - (SanteDB.Core.Api)
The default backup manager

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Backup.DefaultBackupManager, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRequestRestarts : SanteDB.Core.Services.IRequestRestarts { 
	public String ServiceName => "My own IRequestRestarts service";
	/// <summary>
	/// Fired when the backup service requires a restart
	/// </summary>
	public event EventHandler RestartRequested;
}
```

# References

* [IRequestRestarts C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRequestRestarts.htm)
* [InitialConfigurationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Configuration_InitialConfigurationManager.htm)
* [FileConfigurationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_FileConfigurationService.htm)
* [DefaultBackupManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Backup_DefaultBackupManager.htm)
