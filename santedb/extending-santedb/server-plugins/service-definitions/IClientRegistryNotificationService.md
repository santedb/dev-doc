---
description: IClientRegistryNotificationService (SanteDB.Core.Api)
---

## Summary
Represents a client registry notification service.

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyClientRegistryNotificationService : SanteDB.Core.Services.IClientRegistryNotificationService { 
	public String ServiceName => "My own IClientRegistryNotificationService service";
	/// <summary>
	/// Notify that duplicates have been resolved.
	/// </summary>
	public void NotifyDuplicatesResolved(SanteDB.Core.Event.NotificationEventArgs<SanteDB.Core.Model.Roles.Patient> eventArgs){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Notify that a registration occurred.
	/// </summary>
	public void NotifyRegister(SanteDB.Core.Event.NotificationEventArgs<SanteDB.Core.Model.Roles.Patient> eventArgs){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Notify that an update occurred.
	/// </summary>
	public void NotifyUpdate(SanteDB.Core.Event.NotificationEventArgs<SanteDB.Core.Model.Roles.Patient> eventArgs){
		throw new System.NotImplementedException();
	}
}
```
