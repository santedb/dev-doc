---
description: IRoleProviderService (SanteDB.Core.Api)
---

## Summary
Represents a service which is capableof retrieving roles

## Implementations


### ADO.NET Role Provider Service - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoRoleProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyRoleProviderService : SanteDB.Core.Security.Services.IRoleProviderService { 
	public String ServiceName => "My own IRoleProviderService service";
	/// <summary>
	/// Creates a role
	/// </summary>
	public void CreateRole(System.String roleName,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add users to roles
	/// </summary>
	public void AddUsersToRoles(System.String[] users,System.String[] roles,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove users from specified roles
	/// </summary>
	public void RemoveUsersFromRoles(System.String[] users,System.String[] roles,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find all users in a specified role
	/// </summary>
	public System.String[] FindUsersInRole(System.String role){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all roles
	/// </summary>
	public System.String[] GetAllRoles(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all roles
	/// </summary>
	public System.String[] GetAllRoles(System.String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// User user in the specified role
	/// </summary>
	public System.Boolean IsUserInRole(System.String userName,System.String roleName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// User user in the specified role
	/// </summary>
	public System.Boolean IsUserInRole(System.Security.Principal.IPrincipal principal,System.String roleName){
		throw new System.NotImplementedException();
	}
}
```
