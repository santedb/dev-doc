`INotificationService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a notification service which manages the sending of a notification

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Relays|IEnumerable&lt;INotificationRelay>|R|Gets the notification relays available (SMS, EMAIL, etc.)|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetNotificationRelay|INotificationRelay|*Uri* **toAddress**|Gets the specified notification relay|
|GetNotificationRelay|INotificationRelay|*String* **toAddress**|Gets the specified notification relay|
|SendNotification|Guid[]|*String[]* **to**<br/>*String* **subject**<br/>*String* **body**<br/>*Nullable&lt;DateTimeOffset>* **scheduleDelivery**<br/>*Boolean* **ccAdmins**<br/>*NotificationAttachment[]* **attachments**|Send a notification to one or more addresses.|
|SendTemplatedNotification|Guid[]|*String[]* **to**<br/>*String* **templateId**<br/>*String* **templateLanguage**<br/>*Object* **templateModel**<br/>*Nullable&lt;DateTimeOffset>* **scheduleDelivery**<br/>*Boolean* **ccAdmins**<br/>*NotificationAttachment[]* **attachments**|Send a notification using a template to one or more addresses.|

# Implementations


## DefaultNotificationService - (SanteDB.Core.Api)
Default notification relay service that scans the current appdomain for relays

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Notifications.DefaultNotificationService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Notifications;
/// Other usings here
public class MyNotificationService : SanteDB.Core.Notifications.INotificationService { 
	public String ServiceName => "My own INotificationService service";
	/// <summary>
	/// Gets the notification relays available (SMS, EMAIL, etc.)
	/// </summary>
	public IEnumerable<INotificationRelay> Relays {
		get;
	}
	/// <summary>
	/// Gets the specified notification relay
	/// </summary>
	public INotificationRelay GetNotificationRelay(Uri toAddress){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified notification relay
	/// </summary>
	public INotificationRelay GetNotificationRelay(String toAddress){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Send a notification to one or more addresses.
	/// </summary>
	public Guid[] SendNotification(String[] to,String subject,String body,Nullable<DateTimeOffset> scheduleDelivery,Boolean ccAdmins,NotificationAttachment[] attachments){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Send a notification using a template to one or more addresses.
	/// </summary>
	public Guid[] SendTemplatedNotification(String[] to,String templateId,String templateLanguage,Object templateModel,Nullable<DateTimeOffset> scheduleDelivery,Boolean ccAdmins,NotificationAttachment[] attachments){
		throw new System.NotImplementedException();
	}
}
```

# References

* [INotificationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_INotificationService.htm)
* [DefaultNotificationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_DefaultNotificationService.htm)
