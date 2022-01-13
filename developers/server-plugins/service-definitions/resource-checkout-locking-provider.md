`IResourceCheckoutService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
A resource locking service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Checkout|Boolean|*Guid* **key**|Try to get a lock on the resource for editing|
|Checkin|Boolean|*Guid* **key**|Release the lock on the specified key|

# Implementations


## CachedResourceCheckoutService - (SanteDB.Core.Api)
A checkout service which uses the current adhoc cache to manage checkouts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.CachedResourceCheckoutService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyResourceCheckoutService : SanteDB.Core.Services.IResourceCheckoutService { 
	public String ServiceName => "My own IResourceCheckoutService service";
	/// <summary>
	/// Try to get a lock on the resource for editing
	/// </summary>
	public Boolean Checkout<T>(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Release the lock on the specified key
	/// </summary>
	public Boolean Checkin<T>(Guid key){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IResourceCheckoutService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IResourceCheckoutService.htm)
* [CachedResourceCheckoutService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_CachedResourceCheckoutService.htm)
