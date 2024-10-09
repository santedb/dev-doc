`ICertificateGeneratorService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which is responsible for creating and enroling certificates

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateKeyPair|RSAParameters|*Int32* **keyLength**|Create a private key|
|CreateSigningRequest|Byte[]|*RSAParameters* **keyPair**<br/>*X500DistinguishedName* **dn**<br/>*X509KeyUsageFlags* **usageFlags**<br/>*String[]* **enhancedUsages**<br/>*String[]* **alternateNames**|Create a signing request data|
|CreateSelfSignedCertificate|X509Certificate2|*RSAParameters* **keyPair**<br/>*X500DistinguishedName* **dn**<br/>*TimeSpan* **validityPeriod**<br/>*X509KeyUsageFlags* **usageFlags**<br/>*String[]* **enhancedUsages**<br/>*String[]* **alternateNames**<br/>*String* **friendlyName**|Creates a self-signed certificate|
|Combine|X509Certificate2|*X509Certificate2* **certificate**<br/>*RSAParameters* **keyParameters**<br/>*String* **friendlyName**|Combines the  with the|

# Implementations


## BouncyCastleCertificateGenerator - (SanteDB.Security.Certs.BouncyCastle)


### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Security.Certs.BouncyCastle.BouncyCastleCertificateGenerator, SanteDB.Security.Certs.BouncyCastle, Version=3.0.1982.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Certs;
/// Other usings here
public class MyCertificateGeneratorService : SanteDB.Core.Security.Certs.ICertificateGeneratorService { 
	public String ServiceName => "My own ICertificateGeneratorService service";
	/// <summary>
	/// Create a private key
	/// </summary>
	public RSAParameters CreateKeyPair(Int32 keyLength){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a signing request data
	/// </summary>
	public Byte[] CreateSigningRequest(RSAParameters keyPair,X500DistinguishedName dn,X509KeyUsageFlags usageFlags,String[] enhancedUsages,String[] alternateNames){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Creates a self-signed certificate
	/// </summary>
	public X509Certificate2 CreateSelfSignedCertificate(RSAParameters keyPair,X500DistinguishedName dn,TimeSpan validityPeriod,X509KeyUsageFlags usageFlags,String[] enhancedUsages,String[] alternateNames,String friendlyName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Combines the  with the
	/// </summary>
	public X509Certificate2 Combine(X509Certificate2 certificate,RSAParameters keyParameters,String friendlyName){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICertificateGeneratorService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Certs_ICertificateGeneratorService.htm)
* [BouncyCastleCertificateGenerator C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Security_Certs_BouncyCastle_BouncyCastleCertificateGenerator.htm)
