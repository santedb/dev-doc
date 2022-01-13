---
description: User Notification Template Provider (INotificationTemplateFiller in SanteDB.Core.Api)
---

# Summary
Represents a service that can fill the template

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FillTemplate|NotificationTemplate|*String* **id**<br/>*String* **lang**<br/>*Object* **model**|Fill the template|

# Implementations


## RazorNotificationTemplateFiller - (SanteDB.Server.Core)
Represents a notification template filler that uses Razor engine

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Notifications.Templating.RazorNotificationTemplateFiller, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Notifications;
/// Other usings here
public class MyNotificationTemplateFiller : SanteDB.Core.Notifications.INotificationTemplateFiller { 
	public String ServiceName => "My own INotificationTemplateFiller service";
	/// <summary>
	/// Fill the template
	/// </summary>
	public NotificationTemplate FillTemplate(String id,String lang,Object model){
		throw new System.NotImplementedException();
	}
}
```

# References

* [INotificationTemplateFiller C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_INotificationTemplateFiller.htm)
* [RazorNotificationTemplateFiller C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Notifications_Templating_RazorNotificationTemplateFiller.htm)
