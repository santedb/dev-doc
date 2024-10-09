`IDataSigningCertificateManagerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which manages associations between various identities

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AddSigningCertificate|void|*IIdentity* **identity**<br/>*X509Certificate2* **x509Certificate**<br/>*IPrincipal* **principal**|Adds a signing certificate to the identity|
|RemoveSigningCertificate|void|*IIdentity* **identity**<br/>*X509Certificate2* **x509Certificate**<br/>*IPrincipal* **principal**|Removes a signing certificate from an identity|
|GetSigningCertificates|IEnumerable&lt;X509Certificate2>|*IIdentity* **identity**|Gets signing certificates associated with|
|GetSigningCertificates|IEnumerable&lt;X509Certificate2>|*Type* **classOfIdentity**<br/>*NameValueCollection* **filter**|Gets signing certificates associated with|
|TryGetSigningCertificateByThumbprint|Boolean|*String* **x509Thumbprint**<br/>*X509Certificate2&* **certificate**|Get any configured signing certificate based on the thumbprint|
|TryGetSigningCertificateByHash|Boolean|*Byte[]* **x509hash**<br/>*X509Certificate2&* **certificate**|Get configured certificate by hash|
|GetCertificateIdentities|IEnumerable&lt;IIdentity>|*X509Certificate2* **certificate**|Get all associated identities for the provided|

# Implementations


## BridgedDataSigningCertificateManager - (SanteDB.Client)
Implementation of [IDataSigningCertificateManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDataSigningCertificateManagerService.htm) which uses local and fallback to upstream

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.BridgedDataSigningCertificateManager, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UpstreamCertificateAssociationManager - (SanteDB.Client)
Upstream implementation of the certificate association manager

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.UpstreamCertificateAssociationManager, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoDataSigningCertificateManagerService - (SanteDB.Persistence.Data)
ADO data signing certificate

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoDataSigningCertificateManagerService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyDataSigningCertificateManagerService : SanteDB.Core.Security.Services.IDataSigningCertificateManagerService { 
	public String ServiceName => "My own IDataSigningCertificateManagerService service";
	/// <summary>
	/// Adds a signing certificate to the identity
	/// </summary>
	public void AddSigningCertificate(IIdentity identity,X509Certificate2 x509Certificate,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a signing certificate from an identity
	/// </summary>
	public void RemoveSigningCertificate(IIdentity identity,X509Certificate2 x509Certificate,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets signing certificates associated with
	/// </summary>
	public IEnumerable<X509Certificate2> GetSigningCertificates(IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets signing certificates associated with
	/// </summary>
	public IEnumerable<X509Certificate2> GetSigningCertificates(Type classOfIdentity,NameValueCollection filter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get any configured signing certificate based on the thumbprint
	/// </summary>
	public Boolean TryGetSigningCertificateByThumbprint(String x509Thumbprint,X509Certificate2& certificate){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get configured certificate by hash
	/// </summary>
	public Boolean TryGetSigningCertificateByHash(Byte[] x509hash,X509Certificate2& certificate){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all associated identities for the provided
	/// </summary>
	public IEnumerable<IIdentity> GetCertificateIdentities(X509Certificate2 certificate){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataSigningCertificateManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDataSigningCertificateManagerService.htm)
* [BridgedDataSigningCertificateManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_BridgedDataSigningCertificateManager.htm)
* [UpstreamCertificateAssociationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_UpstreamCertificateAssociationManager.htm)
* [AdoDataSigningCertificateManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoDataSigningCertificateManagerService.htm)
