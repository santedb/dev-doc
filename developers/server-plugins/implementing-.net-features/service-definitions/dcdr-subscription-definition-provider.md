`ISubscriptionRepository` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a repository which maintains subscription definitions

## Description
This service is used to maintain instances of [SubscriptionDefinition](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Subscription_SubscriptionDefinition.htm) which 
            contain SQL (or other query grammar) to allow dCDR instances to easily query data on the HDSI interface
            using the ```_subscription``` parameter. The HDSI maps the subscription ID with the local data provider
            and then executes the appopriate query against the persistence layer to ensure fast synchronization of
            new data.

# Implementations


## AppletSubscriptionRepository - (SanteDB.Core.Applets)
An implementation of the [ISubscriptionRepository](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionRepository.htm) that loads definitions from applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletSubscriptionRepository, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySubscriptionRepository : SanteDB.Core.Services.ISubscriptionRepository { 
	public String ServiceName => "My own ISubscriptionRepository service";
}
```

# References

* [ISubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionRepository.htm)
* [AppletSubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletSubscriptionRepository.htm)
