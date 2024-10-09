`IDataSigningService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Contract for services which can sign data using configured digital signature algorithms

## Description
Implementers of this service contract are responsible for computing and validating
            digital signatures against arbitrary data streams. Implementers of this service are responsible for 
            maintaining (or acquiring) a master list of keys which can be used for data signing, and validating 
            digital signatures.

Implementers should also use the [IDataSigningCertificateManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDataSigningCertificateManagerService.htm) to support key identifiers which are indicated as a 
            secure application/device identifier

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetNamedSignatureSettings|SignatureSettings|*String* **systemKeyId**|Get the siganture algorithm for the system configured key|
|GetSignatureSettings|SignatureSettings|*Byte[]* **certificateThumbprint**<br/>*SignatureAlgorithm* **signatureAlgorithm**|Get the signature algorithm for the configured thumbprint|
|SignData|Byte[]|*Byte[]* **data**<br/>*String* **systemKeyId**|Sign  with the configured system key|
|SignData|Byte[]|*Byte[]* **data**<br/>*SignatureSettings* **settings**|Sign  with the configured system key|
|Verify|Boolean|*Byte[]* **data**<br/>*Byte[]* **signature**<br/>*String* **systemKeyId**|Verifies the digital signature of the data|
|Verify|Boolean|*Byte[]* **data**<br/>*Byte[]* **signature**<br/>*SignatureSettings* **settings**|Verifies the digital signature of the data|

# Implementations


## DefaultDataSigningService - (SanteDB.Core.Api)
Default data signing service
### Description
This digital signature service uses the keys configured in the [SecurityConfigurationSection](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Configuration_SecurityConfigurationSection.htm)
            to sign data based on the type of signature algorithm in the [SecurityConfigurationSection](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Configuration_SecurityConfigurationSection.htm). Supported signature 
            algorithms are:

* HMAC256 (HMAC + SHA256) using shared secrets
* RS256 (RSA+SHA256) using X.509 certificates (generation of a signature requires private key)
* RS512 (RSA+SHA512)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultDataSigningService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyDataSigningService : SanteDB.Core.Security.Services.IDataSigningService { 
	public String ServiceName => "My own IDataSigningService service";
	/// <summary>
	/// Get the siganture algorithm for the system configured key
	/// </summary>
	public SignatureSettings GetNamedSignatureSettings(String systemKeyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the signature algorithm for the configured thumbprint
	/// </summary>
	public SignatureSettings GetSignatureSettings(Byte[] certificateThumbprint,SignatureAlgorithm signatureAlgorithm){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Sign  with the configured system key
	/// </summary>
	public Byte[] SignData(Byte[] data,String systemKeyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Sign  with the configured system key
	/// </summary>
	public Byte[] SignData(Byte[] data,SignatureSettings settings){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Verifies the digital signature of the data
	/// </summary>
	public Boolean Verify(Byte[] data,Byte[] signature,String systemKeyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Verifies the digital signature of the data
	/// </summary>
	public Boolean Verify(Byte[] data,Byte[] signature,SignatureSettings settings){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataSigningService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDataSigningService.htm)
* [DefaultDataSigningService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_DefaultDataSigningService.htm)
