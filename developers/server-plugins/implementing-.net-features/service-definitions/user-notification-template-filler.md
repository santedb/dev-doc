`INotificationTemplateFiller` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service that can fill the template

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FillTemplate|NotificationTemplate|*String* **id**<br/>*String* **lang**<br/>*Object* **model**|Fill the template|

# Implementations


## SimpleNotificationTemplateFiller - (SanteDB.Core.Api)
A simple notification template filler that uses ${value} for inputs

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Notifications.Templating.SimpleNotificationTemplateFiller, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
* [SimpleNotificationTemplateFiller C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_Templating_SimpleNotificationTemplateFiller.htm)
