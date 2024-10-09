`INotificationTemplateRepository` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which takes / provides structured templates into structured message objects

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Insert|NotificationTemplate|*NotificationTemplate* **template**|Insert the specified template|
|Update|NotificationTemplate|*NotificationTemplate* **template**|Updates the specified template|
|Get|NotificationTemplate|*String* **id**<br/>*String* **lang**|Gets the specified template|
|Find|IEnumerable&lt;NotificationTemplate>|*Expression&lt;Func&lt;NotificationTemplate,Boolean>>* **filter**|Find the specified template|

# Implementations


## AppletNotificationTemplateRepository - (SanteDB.Core.Applets)
An implementation of the [INotificationTemplateRepository](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_INotificationTemplateRepository.htm) which loads [NotificationTemplate](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_NotificationTemplate.htm) instances
            from the ```notification/``` folder in applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletNotificationTemplateRepository, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Notifications;
/// Other usings here
public class MyNotificationTemplateRepository : SanteDB.Core.Notifications.INotificationTemplateRepository { 
	public String ServiceName => "My own INotificationTemplateRepository service";
	/// <summary>
	/// Insert the specified template
	/// </summary>
	public NotificationTemplate Insert(NotificationTemplate template){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Updates the specified template
	/// </summary>
	public NotificationTemplate Update(NotificationTemplate template){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified template
	/// </summary>
	public NotificationTemplate Get(String id,String lang){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find the specified template
	/// </summary>
	public IEnumerable<NotificationTemplate> Find(Expression<Func<NotificationTemplate,Boolean>> filter){
		throw new System.NotImplementedException();
	}
}
```

# References

* [INotificationTemplateRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_INotificationTemplateRepository.htm)
* [AppletNotificationTemplateRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletNotificationTemplateRepository.htm)
