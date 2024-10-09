`ICertificateSigningService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Certificate signing service (can sign certificates with other certificates)

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|SignCertificateRequest|X509Certificate2|*Byte[]* **request**<br/>*X509Certificate2* **signWithCertificate**|Signs  with|
|GetSigningCertificates|IEnumerable&lt;X509Certificate2>|*none*|TODO|
|GetSigningRequestDN|X500DistinguishedName|*Byte[]* **request**|Parse the signing request and return the DN|

# Implementations


## BouncyCastleCertificateSigner - (SanteDB.Security.Certs.BouncyCastle)
Bouncy castle certificate signing service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Security.Certs.BouncyCastle.BouncyCastleCertificateSigner, SanteDB.Security.Certs.BouncyCastle, Version=3.0.1982.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Certs;
/// Other usings here
public class MyCertificateSigningService : SanteDB.Core.Security.Certs.ICertificateSigningService { 
	public String ServiceName => "My own ICertificateSigningService service";
	/// <summary>
	/// Signs  with
	/// </summary>
	public X509Certificate2 SignCertificateRequest(Byte[] request,X509Certificate2 signWithCertificate){
		throw new System.NotImplementedException();
	}
	public IEnumerable<X509Certificate2> GetSigningCertificates(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Parse the signing request and return the DN
	/// </summary>
	public X500DistinguishedName GetSigningRequestDN(Byte[] request){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICertificateSigningService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Certs_ICertificateSigningService.htm)
* [BouncyCastleCertificateSigner C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Security_Certs_BouncyCastle_BouncyCastleCertificateSigner.htm)
