`ISessionTokenResolverService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Session token resolver service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetEncodedIdToken|String|*ISession* **session**|Get the encoded id token of the  instance provided.|
|GetEncodedRefreshToken|String|*ISession* **session**|Get the encoded refresh token of the  instance provided.|
|GetSessionFromBearerToken|ISession|*String* **encodedToken**|Resolves the session associated with the ID token provided in .|
|ExtendSessionWithRefreshToken|ISession|*String* **encodedToken**|Resolves the session associated with the Refresh token provided in .|

# Implementations


## SimpleSessionTokenResolver - (SanteDB.Core.Api)
Implementation of a session token resolver service which produces a simple pointer to a session identifier

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.Services.SimpleSessionTokenResolver, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MySessionTokenResolverService : SanteDB.Core.Security.Services.ISessionTokenResolverService { 
	public String ServiceName => "My own ISessionTokenResolverService service";
	/// <summary>
	/// Get the encoded id token of the  instance provided.
	/// </summary>
	public String GetEncodedIdToken(ISession session){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the encoded refresh token of the  instance provided.
	/// </summary>
	public String GetEncodedRefreshToken(ISession session){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Resolves the session associated with the ID token provided in .
	/// </summary>
	public ISession GetSessionFromBearerToken(String encodedToken){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Resolves the session associated with the Refresh token provided in .
	/// </summary>
	public ISession ExtendSessionWithRefreshToken(String encodedToken){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISessionTokenResolverService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionTokenResolverService.htm)
* [SimpleSessionTokenResolver C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_SimpleSessionTokenResolver.htm)
