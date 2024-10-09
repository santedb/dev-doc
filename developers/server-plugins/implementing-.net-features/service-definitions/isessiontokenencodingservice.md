`ISessionTokenEncodingService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Service which can encode session id and refresh tokens into an opaque format suitable to be roundtripped through an untrusted context

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Encode|String|*Byte[]* **token**|Encodes a token such that the result is an opaque value that is tamper resistant and suitable for transport through an unsecure context.|
|TryDecode|Boolean|*String* **encodedToken**<br/>*Byte[]&* **token**|Attempts to decode a token. Will return a decoded token in  if the result is true, null otherwise.|
|Decode|Byte[]|*String* **encodedToken**|Attempts to decode a token. Will return the decoded token or throw an exception if the encoded token is invalid.|
|ExtractSessionIdentity|Byte[]|*String* **encodedToken**|Extract the identifier of the session from the encoded token without performing validation|

# Implementations


## SimpleSessionTokenEncodingService - (SanteDB.Core.Api)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SimpleSessionTokenEncodingService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MySessionTokenEncodingService : SanteDB.Core.Security.Services.ISessionTokenEncodingService { 
	public String ServiceName => "My own ISessionTokenEncodingService service";
	/// <summary>
	/// Encodes a token such that the result is an opaque value that is tamper resistant and suitable for transport through an unsecure context.
	/// </summary>
	public String Encode(Byte[] token){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Attempts to decode a token. Will return a decoded token in  if the result is true, null otherwise.
	/// </summary>
	public Boolean TryDecode(String encodedToken,Byte[]& token){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Attempts to decode a token. Will return the decoded token or throw an exception if the encoded token is invalid.
	/// </summary>
	public Byte[] Decode(String encodedToken){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Extract the identifier of the session from the encoded token without performing validation
	/// </summary>
	public Byte[] ExtractSessionIdentity(String encodedToken){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISessionTokenEncodingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionTokenEncodingService.htm)
* [SimpleSessionTokenEncodingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_SimpleSessionTokenEncodingService.htm)
