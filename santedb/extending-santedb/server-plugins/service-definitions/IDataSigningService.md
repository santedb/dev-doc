---
description: IDataSigningService (SanteDB.Core.Api)
---

## Summary
Represents a service which can sign arbitrary data

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MyDataSigningService : SanteDB.Core.Security.IDataSigningService { 
	public String ServiceName => "My own IDataSigningService service";
	/// <summary>
	/// Get the siganture algorithm this service would use to sign w/the specified key
	/// </summary>
	public System.String GetSignatureAlgorithm(System.String keyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Signs the specified data using the service's configured signing key
	/// </summary>
	public System.Byte[] SignData(System.Byte[] data,System.String keyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Verifies the digital signature of the data
	/// </summary>
	public System.Boolean Verify(System.Byte[] data,System.Byte[] signature,System.String keyId){
		throw new System.NotImplementedException();
	}
}
```
