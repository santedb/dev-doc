---
description: IClientRegistryNotificationService (SanteDB.Core.Api)
---

## Summary
Represents a client registry notification service.

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|NotifyDuplicatesResolved|void|*NotificationEventArgs&lt;Patient>* **eventArgs**|Notify that duplicates have been resolved.|
|NotifyRegister|void|*NotificationEventArgs&lt;Patient>* **eventArgs**|Notify that a registration occurred.|
|NotifyUpdate|void|*NotificationEventArgs&lt;Patient>* **eventArgs**|Notify that an update occurred.|

## Implementations

None

## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyClientRegistryNotificationService : SanteDB.Core.Services.IClientRegistryNotificationService { 
	public String ServiceName => "My own IClientRegistryNotificationService service";
	/// <summary>
	/// Notify that duplicates have been resolved.
	/// </summary>
	public void NotifyDuplicatesResolved(NotificationEventArgs<Patient> eventArgs){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Notify that a registration occurred.
	/// </summary>
	public void NotifyRegister(NotificationEventArgs<Patient> eventArgs){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Notify that an update occurred.
	/// </summary>
	public void NotifyUpdate(NotificationEventArgs<Patient> eventArgs){
		throw new System.NotImplementedException();
	}
}
```
