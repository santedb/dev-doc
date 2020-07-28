---
description: ISecurityRepositoryService (SanteDB.Core.Api)
---

## Summary
Security repository service is responsible for the maintenance of security entities

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|ChangePassword|SecurityUser|userId <small style='border:solid 1px #aaa'>Guid</small><br/>password <small style='border:solid 1px #aaa'>String</small>|Changes a user's password.|
|GetProviderEntity|Provider|identity <small style='border:solid 1px #aaa'>IIdentity</small>|Gets the specified provider entity from the specified identity|
|CreateUser|SecurityUser|userInfo <small style='border:solid 1px #aaa'>SecurityUser</small><br/>password <small style='border:solid 1px #aaa'>String</small>|Creates a user with a specified password.|
|GetUser|SecurityUser|userName <small style='border:solid 1px #aaa'>String</small>|Get a user by user name|
|GetPolicy|SecurityPolicy|policyOid <small style='border:solid 1px #aaa'>String</small>|Get the specified security policy by OID|
|GetRole|SecurityRole|roleName <small style='border:solid 1px #aaa'>String</small>|Gets a specific role.|
|LockDevice|void|key <small style='border:solid 1px #aaa'>Guid</small>|Locks a device principal|
|LockApplication|void|key <small style='border:solid 1px #aaa'>Guid</small>|Locks an application|
|UnlockDevice|void|key <small style='border:solid 1px #aaa'>Guid</small>|Removes a lock from a device|
|UnlockApplication|void|key <small style='border:solid 1px #aaa'>Guid</small>|Removes a lock from an application|
|GetUser|SecurityUser|identity <small style='border:solid 1px #aaa'>IIdentity</small>|Get a user by user name|
|GetUserEntity|UserEntity|identity <small style='border:solid 1px #aaa'>IIdentity</small>|Get the user entity|
|LockUser|void|userId <small style='border:solid 1px #aaa'>Guid</small>|Locks a specific user.|
|UnlockUser|void|userId <small style='border:solid 1px #aaa'>Guid</small>|Unlocks a specific user.|
|GetProvenance|SecurityProvenance|provenanceId <small style='border:solid 1px #aaa'>Guid</small>|Get the provenance object|
|FindProvenance|IEnumerable&lt;SecurityProvenance>|query <small style='border:solid 1px #aaa'>Expression<Func<SecurityProvenance,Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small><br/>queryId <small style='border:solid 1px #aaa'>Guid</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Find provenance objects matching the specified object|

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
	public SecurityUser ChangePassword(Guid userId,String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified provider entity from the specified identity
	/// </summary>
	public Provider GetProviderEntity(IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Creates a user with a specified password.
	/// </summary>
	public SecurityUser CreateUser(SecurityUser userInfo,String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a user by user name
	/// </summary>
	public SecurityUser GetUser(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified security policy by OID
	/// </summary>
	public SecurityPolicy GetPolicy(String policyOid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets a specific role.
	/// </summary>
	public SecurityRole GetRole(String roleName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Locks a device principal
	/// </summary>
	public void LockDevice(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Locks an application
	/// </summary>
	public void LockApplication(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a lock from a device
	/// </summary>
	public void UnlockDevice(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a lock from an application
	/// </summary>
	public void UnlockApplication(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a user by user name
	/// </summary>
	public SecurityUser GetUser(IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the user entity
	/// </summary>
	public UserEntity GetUserEntity(IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Locks a specific user.
	/// </summary>
	public void LockUser(Guid userId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Unlocks a specific user.
	/// </summary>
	public void UnlockUser(Guid userId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the provenance object
	/// </summary>
	public SecurityProvenance GetProvenance(Guid provenanceId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find provenance objects matching the specified object
	/// </summary>
	public IEnumerable<SecurityProvenance> FindProvenance(Expression<Func<SecurityProvenance,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```
