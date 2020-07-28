---
description: IDataSigningService (SanteDB.Core.Api)
---

## Summary
Represents a service which can sign arbitrary data

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetSignatureAlgorithm|String|*String* **keyId**|Get the siganture algorithm this service would use to sign w/the specified key|
|SignData|Byte[]|*Byte[]* **data**<br/>*String* **keyId**|Signs the specified data using the service's configured signing key|
|Verify|Boolean|*Byte[]* **data**<br/>*Byte[]* **signature**<br/>*String* **keyId**|Verifies the digital signature of the data|

## Implementations


### DefaultDataSigningService - (SanteDB.Core)
Default data signature service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultDataSigningService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MyDataSigningService : SanteDB.Core.Security.IDataSigningService { 
	public String ServiceName => "My own IDataSigningService service";
	/// <summary>
	/// Get the siganture algorithm this service would use to sign w/the specified key
	/// </summary>
	public String GetSignatureAlgorithm(String keyId){
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
