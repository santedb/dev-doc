Data Signing Service (IDataSigningService in SanteDB.Core.Api)

# Summary
Represents a service which can sign arbitrary data

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetKeys|IEnumerable&lt;String>||TODO|
|GetSignatureAlgorithm|String|*String* **keyId**|Get the siganture algorithm this service would use to sign w/the specified key|
|AddSigningKey|void|*String* **keyId**<br/>*Byte[]* **keyData**<br/>*String* **signatureAlgorithm**|Register a key with the provider|
|SignData|Byte[]|*Byte[]* **data**<br/>*String* **keyId**|Signs the specified data using the service's configured signing key|
|Verify|Boolean|*Byte[]* **data**<br/>*Byte[]* **signature**<br/>*String* **keyId**|Verifies the digital signature of the data|

# Implementations


## DefaultDataSigningService - (SanteDB.Server.Core)
Default data signature service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.DefaultDataSigningService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MyDataSigningService : SanteDB.Core.Security.IDataSigningService { 
	public String ServiceName => "My own IDataSigningService service";
	public IEnumerable<String> GetKeys(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the siganture algorithm this service would use to sign w/the specified key
	/// </summary>
	public String GetSignatureAlgorithm(String keyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Register a key with the provider
	/// </summary>
	public void AddSigningKey(String keyId,Byte[] keyData,String signatureAlgorithm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Signs the specified data using the service's configured signing key
	/// </summary>
	public Byte[] SignData(Byte[] data,String keyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Verifies the digital signature of the data
	/// </summary>
	public Boolean Verify(Byte[] data,Byte[] signature,String keyId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataSigningService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_IDataSigningService.htm)
* [DefaultDataSigningService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_DefaultDataSigningService.htm)
