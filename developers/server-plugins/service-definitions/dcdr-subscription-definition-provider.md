`ISubscriptionRepository` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a repository which maintains subscription definitions

## Description
This service is used to maintain instances of [SubscriptionDefinition](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Subscription_SubscriptionDefinition.htm) which 
            contain SQL (or other query grammar) to allow dCDR instances to easily query data on the HDSI interface
            using the ```_subscription``` parameter. The HDSI maps the subscription ID with the local data provider
            and then executes the appopriate query against the persistence layer to ensure fast synchronization of
            new data.

# Implementations

None

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
