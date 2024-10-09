`ICertificateAuthorityService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents an integration to a certificate authority

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|SubmitSigningRequest|ICertificateSigningRequest|*Byte[]* **csr**|Submit a signing request to this authority|
|GetSigningRequests|IEnumerable&lt;ICertificateSigningRequest>|*CertificateSigningRequestStatus* **status**|Get all signing requests for the CA service|
|GetSigningRequest|ICertificateSigningRequest|*String* **csrId**|Get a particular signing request by its identifier|
|FindSigningRequest|ICertificateSigningRequest|*X509FindType* **findType**<br/>*Object* **value**|Find a signing request by the specified identifier|
|DeleteSigningRequest|ICertificateSigningRequest|*String* **csrId**|Delete a signing request by id|
|Approve|X509Certificate2|*ICertificateSigningRequest* **request**|Approve the certificate signing request|
|Reject|void|*ICertificateSigningRequest* **request**|Reject the|
|GetCertificates|IEnumerable&lt;X509Certificate2>|*none*|TODO|
|Revoke|X509Certificate2|*X509Certificate2* **certificate**|Revoke the certificate signing request|
|Renew|X509Certificate2|*X509Certificate2* **certificate**|Renew the specified|
|Find|IEnumerable&lt;X509Certificate2>|*X509FindType* **findType**<br/>*Object* **findValue**|Find the specified certificate in the|
|GetCertificate|X509Certificate2|*ICertificateSigningRequest* **certRequest**|Get the certificate that was generated for|
|GetRevokationList|IEnumerable&lt;X509Certificate2>|*none*|TODO|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Certs;
/// Other usings here
public class MyCertificateAuthorityService : SanteDB.Core.Security.Certs.ICertificateAuthorityService { 
	public String ServiceName => "My own ICertificateAuthorityService service";
	/// <summary>
	/// Submit a signing request to this authority
	/// </summary>
	public ICertificateSigningRequest SubmitSigningRequest(Byte[] csr){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all signing requests for the CA service
	/// </summary>
	public IEnumerable<ICertificateSigningRequest> GetSigningRequests(CertificateSigningRequestStatus status){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a particular signing request by its identifier
	/// </summary>
	public ICertificateSigningRequest GetSigningRequest(String csrId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find a signing request by the specified identifier
	/// </summary>
	public ICertificateSigningRequest FindSigningRequest(X509FindType findType,Object value){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete a signing request by id
	/// </summary>
	public ICertificateSigningRequest DeleteSigningRequest(String csrId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Approve the certificate signing request
	/// </summary>
	public X509Certificate2 Approve(ICertificateSigningRequest request){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Reject the
	/// </summary>
	public void Reject(ICertificateSigningRequest request){
		throw new System.NotImplementedException();
	}
	public IEnumerable<X509Certificate2> GetCertificates(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Revoke the certificate signing request
	/// </summary>
	public X509Certificate2 Revoke(X509Certificate2 certificate){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Renew the specified
	/// </summary>
	public X509Certificate2 Renew(X509Certificate2 certificate){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find the specified certificate in the
	/// </summary>
	public IEnumerable<X509Certificate2> Find(X509FindType findType,Object findValue){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the certificate that was generated for
	/// </summary>
	public X509Certificate2 GetCertificate(ICertificateSigningRequest certRequest){
		throw new System.NotImplementedException();
	}
	public IEnumerable<X509Certificate2> GetRevokationList(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICertificateAuthorityService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Certs_ICertificateAuthorityService.htm)
