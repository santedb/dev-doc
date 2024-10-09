`ISymmetricCryptographicProvider` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a crypto service provider that encrypts things using symmetric encryption

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetContextKey|Byte[]|*none*|TODO|
|RotateContextKey|Boolean|*none*|TODO|
|GenerateIV|Byte[]|*none*|TODO|
|GenerateKey|Byte[]|*none*|TODO|
|Encrypt|Byte[]|*Byte[]* **data**<br/>*Byte[]* **key**<br/>*Byte[]* **iv**|Encrypts the sepcified data|
|Decrypt|Byte[]|*Byte[]* **data**<br/>*Byte[]* **key**<br/>*Byte[]* **iv**|Decrypts the specified data|
|Encrypt|Byte[]|*Byte[]* **data**|Encrypts the sepcified data|
|Decrypt|Byte[]|*Byte[]* **data**|Decrypts the specified data|
|Encrypt|String|*String* **data**|Encrypts the sepcified data|
|Decrypt|String|*String* **data**|Decrypts the specified data|
|CreateEncryptingStream|Stream|*Stream* **underlyingStream**<br/>*Byte[]* **key**<br/>*Byte[]* **iv**|Create a decrypting stream|
|CreateDecryptingStream|Stream|*Stream* **underlyingStream**<br/>*Byte[]* **key**<br/>*Byte[]* **iv**|Create a decrypting stream|

# Implementations


## AesSymmetricCrypographicProvider - (SanteDB.Core.Api)
Represents a symmetric cryptographic provider based on AES

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.AesSymmetricCrypographicProvider, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MySymmetricCryptographicProvider : SanteDB.Core.Security.Services.ISymmetricCryptographicProvider { 
	public String ServiceName => "My own ISymmetricCryptographicProvider service";
	public Byte[] GetContextKey(){
		throw new System.NotImplementedException();
	}
	public Boolean RotateContextKey(){
		throw new System.NotImplementedException();
	}
	public Byte[] GenerateIV(){
		throw new System.NotImplementedException();
	}
	public Byte[] GenerateKey(){
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
	/// <summary>
	/// Encrypts the sepcified data
	/// </summary>
	public Byte[] Encrypt(Byte[] data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Decrypts the specified data
	/// </summary>
	public Byte[] Decrypt(Byte[] data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Encrypts the sepcified data
	/// </summary>
	public String Encrypt(String data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Decrypts the specified data
	/// </summary>
	public String Decrypt(String data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a decrypting stream
	/// </summary>
	public Stream CreateEncryptingStream(Stream underlyingStream,Byte[] key,Byte[] iv){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a decrypting stream
	/// </summary>
	public Stream CreateDecryptingStream(Stream underlyingStream,Byte[] key,Byte[] iv){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISymmetricCryptographicProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISymmetricCryptographicProvider.htm)
* [AesSymmetricCrypographicProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_AesSymmetricCrypographicProvider.htm)
