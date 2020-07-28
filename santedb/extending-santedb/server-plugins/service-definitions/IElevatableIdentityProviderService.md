---
description: IElevatableIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Represents an identity provider that allows for elevation

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyElevatableIdentityProviderService : SanteDB.Core.Security.Services.IElevatableIdentityProviderService { 
	public String ServiceName => "My own IElevatableIdentityProviderService service";
	/// <summary>
	/// The caller has requested an override
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.SecurityOverrideEventArgs> OverrideRequested;
	/// <summary>
	/// Requests the currently established principal to be elevated
	/// </summary>
	public System.Security.Principal.IPrincipal ElevatedAuthenticate(System.String userName,System.String password,System.String tfaSecret,System.String purpose,System.String[] policies){
		throw new System.NotImplementedException();
	}
}
```
