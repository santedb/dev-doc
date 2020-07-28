---
description: ISecurityRepositoryService (SanteDB.Core.Api)
---

## Summary
Security repository service is responsible for the maintenance of security entities

## Implementations


### LocalSecurityRepositoryService - (SanteDB.Core)
Represents a security repository service that uses the direct local services

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalSecurityRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySecurityRepositoryService : SanteDB.Core.Services.ISecurityRepositoryService { 
	public String ServiceName => "My own ISecurityRepositoryService service";
	/// <summary>
	/// Changes a user's password.
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityUser ChangePassword(System.Guid userId,System.String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified provider entity from the specified identity
	/// </summary>
	public SanteDB.Core.Model.Roles.Provider GetProviderEntity(System.Security.Principal.IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Creates a user with a specified password.
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityUser CreateUser(SanteDB.Core.Model.Security.SecurityUser userInfo,System.String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a user by user name
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityUser GetUser(System.String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified security policy by OID
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityPolicy GetPolicy(System.String policyOid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets a specific role.
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityRole GetRole(System.String roleName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Locks a device principal
	/// </summary>
	public void LockDevice(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Locks an application
	/// </summary>
	public void LockApplication(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a lock from a device
	/// </summary>
	public void UnlockDevice(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a lock from an application
	/// </summary>
	public void UnlockApplication(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a user by user name
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityUser GetUser(System.Security.Principal.IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the user entity
	/// </summary>
	public SanteDB.Core.Model.Entities.UserEntity GetUserEntity(System.Security.Principal.IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Locks a specific user.
	/// </summary>
	public void LockUser(System.Guid userId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Unlocks a specific user.
	/// </summary>
	public void UnlockUser(System.Guid userId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the provenance object
	/// </summary>
	public SanteDB.Core.Model.Security.SecurityProvenance GetProvenance(System.Guid provenanceId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find provenance objects matching the specified object
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.Security.SecurityProvenance> FindProvenance(System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Model.Security.SecurityProvenance,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Guid queryId,SanteDB.Core.Model.Query.ModelSort`1[[SanteDB.Core.Model.Security.SecurityProvenance, SanteDB.Core.Model, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null]][] orderBy){
		throw new System.NotImplementedException();
	}
}
```
