`IResourceCheckoutService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
A resource locking service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Checkout|Boolean|*Guid* **key**|Try to get a lock on the resource for editing|
|Checkin|Boolean|*Guid* **key**|Release the lock on the specified key|
|IsCheckedout|Boolean|*Guid* **key**<br/>*IIdentity&* **currentOwner**|Attempts to perform a soft checkout - this is equivalent to attempting to take a lock             but not actually taking it|

# Implementations


## UpstreamResourceCheckoutService - (SanteDB.Client)
A [IResourceCheckoutService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IResourceCheckoutService.htm) which uses the upstream

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Repositories.UpstreamResourceCheckoutService, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CachedResourceCheckoutService - (SanteDB.Core.Api)
A checkout service which uses the current adhoc cache to manage checkouts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.CachedResourceCheckoutService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	/// <summary>
	/// Attempts to perform a soft checkout - this is equivalent to attempting to take a lock             but not actually taking it
	/// </summary>
	public Boolean IsCheckedout<T>(Guid key,IIdentity& currentOwner){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IResourceCheckoutService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IResourceCheckoutService.htm)
* [UpstreamResourceCheckoutService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_UpstreamResourceCheckoutService.htm)
* [CachedResourceCheckoutService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_CachedResourceCheckoutService.htm)
