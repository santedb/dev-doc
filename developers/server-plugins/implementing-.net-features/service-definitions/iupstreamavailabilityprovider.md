`IUpstreamAvailabilityProvider` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Implementers can fetch metadata about the upstream service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetUpstreamLatency|Nullable&lt;Int64>|*ServiceEndpointType* **endpointType**|Determines the application layer latency with the specified endpoint|
|IsAvailable|Boolean|*ServiceEndpointType* **endpoint**|Determines whether the upstream service is available.|
|GetTimeDrift|Nullable&lt;TimeSpan>|*ServiceEndpointType* **endpoint**|Get server time drift between this machine and the server|

# Implementations


## DefaultUpstreamAvailabilityProvider - (SanteDB.Client)
Upstream availability provider

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Management.DefaultUpstreamAvailabilityProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyUpstreamAvailabilityProvider : SanteDB.Core.Services.IUpstreamAvailabilityProvider { 
	public String ServiceName => "My own IUpstreamAvailabilityProvider service";
	/// <summary>
	/// Determines the application layer latency with the specified endpoint
	/// </summary>
	public Nullable<Int64> GetUpstreamLatency(ServiceEndpointType endpointType){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Determines whether the upstream service is available.
	/// </summary>
	public Boolean IsAvailable(ServiceEndpointType endpoint){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get server time drift between this machine and the server
	/// </summary>
	public Nullable<TimeSpan> GetTimeDrift(ServiceEndpointType endpoint){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IUpstreamAvailabilityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IUpstreamAvailabilityProvider.htm)
* [DefaultUpstreamAvailabilityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Management_DefaultUpstreamAvailabilityProvider.htm)
