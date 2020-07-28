---
description: IAssigningAuthorityRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a repository service for managing assigning authorities.

## Implementations


### LocalAssigningAuthorityRepository - (SanteDB.Core)
Represents a repository service for managing assigning authorities.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalAssigningAuthorityRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAssigningAuthorityRepositoryService : SanteDB.Core.Services.IAssigningAuthorityRepositoryService { 
	public String ServiceName => "My own IAssigningAuthorityRepositoryService service";
	/// <summary>
	/// Get by domain
	/// </summary>
	public SanteDB.Core.Model.DataTypes.AssigningAuthority Get(System.String domain){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get by domain
	/// </summary>
	public SanteDB.Core.Model.DataTypes.AssigningAuthority Get(System.Uri uri){
		throw new System.NotImplementedException();
	}
}
```
