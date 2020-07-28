---
description: IClientRegistryNotificationService (SanteDB.Core.Api)
---

## Summary
Represents a client registry notification service.

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|NotifyDuplicatesResolved|void|eventArgs <small style='border:solid 1px #aaa'>NotificationEventArgs<Patient></small>|Notify that duplicates have been resolved.|
|NotifyRegister|void|eventArgs <small style='border:solid 1px #aaa'>NotificationEventArgs<Patient></small>|Notify that a registration occurred.|
|NotifyUpdate|void|eventArgs <small style='border:solid 1px #aaa'>NotificationEventArgs<Patient></small>|Notify that an update occurred.|

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
