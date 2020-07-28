---
description: IRoleProviderService (SanteDB.Core.Api)
---

## Summary
Represents a service which is capableof retrieving roles

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateRole|void|roleName <small style='border:solid 1px #aaa'>String</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Creates a role|
|AddUsersToRoles|void|users <small style='border:solid 1px #aaa'>String[]</small><br/>roles <small style='border:solid 1px #aaa'>String[]</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Add users to roles|
|RemoveUsersFromRoles|void|users <small style='border:solid 1px #aaa'>String[]</small><br/>roles <small style='border:solid 1px #aaa'>String[]</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Remove users from specified roles|
|FindUsersInRole|String[]|role <small style='border:solid 1px #aaa'>String</small>|Find all users in a specified role|
|GetAllRoles|String[]||Get all roles|
|GetAllRoles|String[]|userName <small style='border:solid 1px #aaa'>String</small>|Get all roles|
|IsUserInRole|Boolean|userName <small style='border:solid 1px #aaa'>String</small><br/>roleName <small style='border:solid 1px #aaa'>String</small>|User user in the specified role|
|IsUserInRole|Boolean|principal <small style='border:solid 1px #aaa'>IPrincipal</small><br/>roleName <small style='border:solid 1px #aaa'>String</small>|User user in the specified role|

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
	public void CreateRole(String roleName,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add users to roles
	/// </summary>
	public void AddUsersToRoles(String[] users,String[] roles,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove users from specified roles
	/// </summary>
	public void RemoveUsersFromRoles(String[] users,String[] roles,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find all users in a specified role
	/// </summary>
	public String[] FindUsersInRole(String role){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all roles
	/// </summary>
	public String[] GetAllRoles(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all roles
	/// </summary>
	public String[] GetAllRoles(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// User user in the specified role
	/// </summary>
	public Boolean IsUserInRole(String userName,String roleName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// User user in the specified role
	/// </summary>
	public Boolean IsUserInRole(IPrincipal principal,String roleName){
		throw new System.NotImplementedException();
	}
}
```
