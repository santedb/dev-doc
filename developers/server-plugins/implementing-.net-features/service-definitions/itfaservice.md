`ITfaService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a two-factor authentication relay service

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Mechanisms|IEnumerable&lt;ITfaMechanism>|R|Get TFA mechanisms|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|SendSecret|String|*Guid* **mechanismId**<br/>*IIdentity* **user**|Send the secret for the specified user|
|ValidateSecret|Boolean|*Guid* **mechanismId**<br/>*IIdentity* **user**<br/>*String* **secret**|Send the secret for the specified user|

# Implementations


## UpstreamTfaService - (SanteDB.Client)
A TFA service which communicates with the upstream

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.UpstreamTfaService, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Default TFA Provider - (SanteDB.Core.Api)
Represents a default implementation of a TFA relay service which scans the entire application domain for
            mechanisms and allows calling of them all

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultTfaService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyTfaService : SanteDB.Core.Security.Services.ITfaService { 
	public String ServiceName => "My own ITfaService service";
	/// <summary>
	/// Get TFA mechanisms
	/// </summary>
	public IEnumerable<ITfaMechanism> Mechanisms {
		get;
	}
	/// <summary>
	/// Send the secret for the specified user
	/// </summary>
	public String SendSecret(Guid mechanismId,IIdentity user){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Send the secret for the specified user
	/// </summary>
	public Boolean ValidateSecret(Guid mechanismId,IIdentity user,String secret){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ITfaService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ITfaService.htm)
* [UpstreamTfaService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_UpstreamTfaService.htm)
* [DefaultTfaService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_DefaultTfaService.htm)
