ISecurityRepositoryService (ISecurityRepositoryService in SanteDB.Core.Api)

# Summary
Security repository service is responsible for the maintenance of security entities

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|ChangePassword|SecurityUser|*Guid* **userId**<br/>*String* **password**|Changes a user's password.|
|GetProviderEntity|Provider|*IIdentity* **identity**|Gets the specified provider entity from the specified identity|
|CreateUser|SecurityUser|*SecurityUser* **userInfo**<br/>*String* **password**|Creates a user with a specified password.|
|GetUser|SecurityUser|*String* **userName**|Get a user by user name|
|GetDevice|SecurityDevice|*String* **deviceName**|Get a device by name|
|GetApplication|SecurityApplication|*String* **applicationName**|Get a app by name|
|GetPolicy|SecurityPolicy|*String* **policyOid**|Get the specified security policy by OID|
|GetRole|SecurityRole|*String* **roleName**|Gets a specific role.|
|LockDevice|void|*Guid* **key**|Locks a device principal|
|LockApplication|void|*Guid* **key**|Locks an application|
|UnlockDevice|void|*Guid* **key**|Removes a lock from a device|
|UnlockApplication|void|*Guid* **key**|Removes a lock from an application|
|GetUser|SecurityUser|*IIdentity* **identity**|Get a user by user name|
|GetDevice|SecurityDevice|*IIdentity* **identity**|Get a device by name|
|GetApplication|SecurityApplication|*IIdentity* **identity**|Get a app by name|
|GetUserEntity|UserEntity|*IIdentity* **identity**|Get the user entity|
|LockUser|void|*Guid* **userId**|Locks a specific user.|
|UnlockUser|void|*Guid* **userId**|Unlocks a specific user.|
|GetProvenance|SecurityProvenance|*Guid* **provenanceId**|Get the provenance object|
|GetSecurityEntity|SecurityEntity|*IPrincipal* **principal**|Get the data object for the provided|
|FindProvenance|IEnumerable&lt;SecurityProvenance>|*Expression&lt;Func&lt;SecurityProvenance,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**<br/>*ModelSort`1[]* **orderBy**|Find provenance objects matching the specified object|

# Implementations


## LocalSecurityRepositoryService - (SanteDB.Server.Core)
Represents a security repository service that uses the direct local services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalSecurityRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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
	/// Get a device by name
	/// </summary>
	public SecurityDevice GetDevice(String deviceName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a app by name
	/// </summary>
	public SecurityApplication GetApplication(String applicationName){
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
	/// Get a device by name
	/// </summary>
	public SecurityDevice GetDevice(IIdentity identity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a app by name
	/// </summary>
	public SecurityApplication GetApplication(IIdentity identity){
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
	/// Get the data object for the provided
	/// </summary>
	public SecurityEntity GetSecurityEntity(IPrincipal principal){
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

# References

* [ISecurityRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISecurityRepositoryService.htm)
* [LocalSecurityRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalSecurityRepositoryService.htm)
