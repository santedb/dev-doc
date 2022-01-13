Symmetric Encryption Provider (ISymmetricCryptographicProvider in SanteDB.Core.Api)

# Summary
Represents a crypto service provider that encrypts things using symmetric encryption

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GenerateIV|Byte[]||TODO|
|GenerateKey|Byte[]||TODO|
|GetContextKey|Byte[]||TODO|
|Encrypt|Byte[]|*Byte[]* **data**<br/>*Byte[]* **key**<br/>*Byte[]* **iv**|Encrypts the sepcified data|
|Decrypt|Byte[]|*Byte[]* **data**<br/>*Byte[]* **key**<br/>*Byte[]* **iv**|Decrypts the specified data|

# Implementations


## AesSymmetricCrypographicProvider - (SanteDB.Server.Core)
Represents a symmetric cryptographic provider based on AES

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.AesSymmetricCrypographicProvider, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MySymmetricCryptographicProvider : SanteDB.Core.Security.ISymmetricCryptographicProvider { 
	public String ServiceName => "My own ISymmetricCryptographicProvider service";
	public Byte[] GenerateIV(){
		throw new System.NotImplementedException();
	}
	public Byte[] GenerateKey(){
		throw new System.NotImplementedException();
	}
	public Byte[] GetContextKey(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Encrypts the sepcified data
	/// </summary>
	public Byte[] Encrypt(Byte[] data,Byte[] key,Byte[] iv){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Decrypts the specified data
	/// </summary>
	public Byte[] Decrypt(Byte[] data,Byte[] key,Byte[] iv){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISymmetricCryptographicProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_ISymmetricCryptographicProvider.htm)
* [AesSymmetricCrypographicProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_AesSymmetricCrypographicProvider.htm)
