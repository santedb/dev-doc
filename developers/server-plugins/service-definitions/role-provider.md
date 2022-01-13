`IRoleProviderService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a service which is capableof retrieving roles

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateRole|void|*String* **roleName**<br/>*IPrincipal* **principal**|Creates a role|
|AddUsersToRoles|void|*String[]* **users**<br/>*String[]* **roles**<br/>*IPrincipal* **principal**|Add users to roles|
|RemoveUsersFromRoles|void|*String[]* **users**<br/>*String[]* **roles**<br/>*IPrincipal* **principal**|Remove users from specified roles|
|FindUsersInRole|String[]|*String* **role**|Find all users in a specified role|
|GetAllRoles|String[]|*none*|Get all roles|
|GetAllRoles|String[]|*String* **userName**|Get all roles|
|IsUserInRole|Boolean|*String* **userName**<br/>*String* **roleName**|User user in the specified role|

# Implementations


## ADO.NET Role Provider Service - (SanteDB.Persistence.Data.ADO)
Local role provider

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoRoleProvider, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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
}
```

# References

* [IRoleProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IRoleProviderService.htm)
* [AdoRoleProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoRoleProvider.htm)
