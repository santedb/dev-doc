`IBackupService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service that can back-up data to/from another location

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Backup|IBackupDescriptor|*BackupMedia* **media**<br/>*String* **password**|Backup media|
|Restore|Boolean|*BackupMedia* **media**<br/>*String* **backupDescriptorLabel**<br/>*String* **password**|Restore from media|
|HasBackup|Boolean|*BackupMedia* **media**|Has backup on the specified media|
|GetBackupDescriptors|IEnumerable&lt;IBackupDescriptor>|*BackupMedia* **media**|Gets the backup descriptors for the specified media|
|GetBackupAssetClasses|IDictionary&lt;Guid,Type>|*none*|TODO|
|RemoveBackup|void|*BackupMedia* **media**<br/>*String* **backupDescriptorLabel**|Remove a backup|
|GetBackup|IBackupDescriptor|*BackupMedia* **media**<br/>*String* **backupDescriptorLabel**|Get the descriptor for a specific backup|
|GetBackup|IBackupDescriptor|*String* **backupDescriptorLabel**<br/>*BackupMedia&* **locatedOnMedia**|Get the descriptor for a specific backup|

# Implementations


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
using SanteDB.Core.Data.Backup;
/// Other usings here
public class MyBackupService : SanteDB.Core.Data.Backup.IBackupService { 
	public String ServiceName => "My own IBackupService service";
	/// <summary>
	/// Backup media
	/// </summary>
	public IBackupDescriptor Backup(BackupMedia media,String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Restore from media
	/// </summary>
	public Boolean Restore(BackupMedia media,String backupDescriptorLabel,String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Has backup on the specified media
	/// </summary>
	public Boolean HasBackup(BackupMedia media){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the backup descriptors for the specified media
	/// </summary>
	public IEnumerable<IBackupDescriptor> GetBackupDescriptors(BackupMedia media){
		throw new System.NotImplementedException();
	}
	public IDictionary<Guid,Type> GetBackupAssetClasses(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove a backup
	/// </summary>
	public void RemoveBackup(BackupMedia media,String backupDescriptorLabel){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the descriptor for a specific backup
	/// </summary>
	public IBackupDescriptor GetBackup(BackupMedia media,String backupDescriptorLabel){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the descriptor for a specific backup
	/// </summary>
	public IBackupDescriptor GetBackup(String backupDescriptorLabel,BackupMedia& locatedOnMedia){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBackupService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Backup_IBackupService.htm)
* [DefaultBackupManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Backup_DefaultBackupManager.htm)
