---
description: IRepositoryService`1 (IRepositoryService<TModel> in SanteDB.Core.Api)
---

# Summary
Represents a repository service base

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|TModel|*Guid* **key**|Gets the specified model.|
|Get|TModel|*Guid* **key**<br/>*Guid* **versionKey**|Gets the specified model.|
|Find|IEnumerable&lt;TModel>|*Expression&lt;Func&lt;TModel,Boolean>>* **query**|Finds the specified data.|
|Find|IEnumerable&lt;TModel>|*Expression&lt;Func&lt;TModel,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*ModelSort`1[]* **orderBy**|Finds the specified data.|
|Insert|TModel|*TModel* **data**|Inserts the specified data.|
|Save|TModel|*TModel* **data**|Saves the specified data.|
|Obsolete|TModel|*Guid* **key**|Obsoletes the specified data.|

# Implementations


## AppletSubscriptionRepository - (SanteDB.Core.Applets)
An implementation of the ISubscriptionRepository that loads definitions from applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletSubscriptionRepository, SanteDB.Core.Applets, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalActRepository`1 - (SanteDB.Server.Core)
Represents an act repository service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalActRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalClinicalDataRepository`1 - (SanteDB.Server.Core)
Represents generic local clinical data repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalClinicalDataRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalConceptRepository`1 - (SanteDB.Server.Core)
Generic local concept repository with sufficient permissions

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalConceptRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalRepositoryEx`1 - (SanteDB.Server.Core)
Generic nullifiable local repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalRepositoryEx`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalSecurityRepository`1 - (SanteDB.Server.Core)
Generic local security repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalSecurityRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalEntityRelationshipRepository - (SanteDB.Server.Core)
Represents a local entity relationship repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalEntityRelationshipRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalExtensionTypeRepository - (SanteDB.Server.Core)
Local extension types

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalExtensionTypeRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalManufacturedMaterialRepository - (SanteDB.Server.Core)
Local material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalManufacturedMaterialRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalPatientRepository - (SanteDB.Server.Core)
Local material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalPatientRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalProviderRepository - (SanteDB.Server.Core)
Provides operations for managing organizations.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalProviderRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local Mail Message - (SanteDB.Server.Core)
Represents a local alert service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalMailMessageRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalAssigningAuthorityRepository - (SanteDB.Server.Core)
Represents a repository service for managing assigning authorities.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalAssigningAuthorityRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Default Audit Repository - (SanteDB.Server.Core)
Represents an audit repository which stores and queries audit data.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalAuditRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalBatchRepository - (SanteDB.Server.Core)
Local batch repository service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalBatchRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local Repository Service - (SanteDB.Server.Core)
Represents a base class for entity repository services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalMetadataRepository`1 - (SanteDB.Server.Core)
Provides generic basis for metadata editing

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalMetadataRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalMaterialRepository - (SanteDB.Server.Core)
Local material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalMaterialRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityApplicationRepository - (SanteDB.Server.Core)
Local security application repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalSecurityApplicationRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityDeviceRepository - (SanteDB.Server.Core)
Local security device repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalSecurityDeviceRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityPolicyRepository - (SanteDB.Server.Core)
Alter policies

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalSecurityPolicyRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityRoleRepositoryService - (SanteDB.Server.Core)
Represents a local security role service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalSecurityRoleRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityUserRepositoryService - (SanteDB.Server.Core)
Security user repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalSecurityUserRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalTemplateDefinitionRepositoryService - (SanteDB.Server.Core)
Represents a local metadata repository service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalTemplateDefinitionRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalOrganizationRepository - (SanteDB.Server.Core)
Provides operations for managing organizations.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalOrganizationRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalPlaceRepository - (SanteDB.Server.Core)
Place repository that uses local persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalPlaceRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalUserEntityRepository - (SanteDB.Server.Core)
Localuser entity repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalUserEntityRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalConceptRepository - (SanteDB.Server.Core)
Represents a service which is responsible for the
            maintenance of concepts.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalConceptRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRepositoryService<TModel> : SanteDB.Core.Services.IRepositoryService<TModel> { 
	public String ServiceName => "My own IRepositoryService`1 service";
	/// <summary>
	/// Gets the specified model.
	/// </summary>
	public TModel Get(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified model.
	/// </summary>
	public TModel Get(Guid key,Guid versionKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data.
	/// </summary>
	public IEnumerable<TModel> Find(Expression<Func<TModel,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data.
	/// </summary>
	public IEnumerable<TModel> Find(Expression<Func<TModel,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts the specified data.
	/// </summary>
	public TModel Insert(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Saves the specified data.
	/// </summary>
	public TModel Save(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Obsoletes the specified data.
	/// </summary>
	public TModel Obsolete(Guid key){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IRepositoryService`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService`1.htm)
* [AppletSubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletSubscriptionRepository.htm)
* [GenericLocalActRepository`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalActRepository`1.htm)
* [GenericLocalClinicalDataRepository`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalClinicalDataRepository`1.htm)
* [GenericLocalConceptRepository`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalConceptRepository`1.htm)
* [GenericLocalRepositoryEx`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalRepositoryEx`1.htm)
* [GenericLocalSecurityRepository`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalSecurityRepository`1.htm)
* [LocalEntityRelationshipRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalEntityRelationshipRepository.htm)
* [LocalExtensionTypeRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalExtensionTypeRepository.htm)
* [LocalManufacturedMaterialRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalManufacturedMaterialRepository.htm)
* [LocalPatientRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalPatientRepository.htm)
* [LocalProviderRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalProviderRepository.htm)
* [LocalMailMessageRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalMailMessageRepository.htm)
* [LocalAssigningAuthorityRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalAssigningAuthorityRepository.htm)
* [LocalAuditRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalAuditRepository.htm)
* [LocalBatchRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalBatchRepository.htm)
* [GenericLocalRepository`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalRepository`1.htm)
* [GenericLocalMetadataRepository`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalMetadataRepository`1.htm)
* [LocalMaterialRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalMaterialRepository.htm)
* [LocalSecurityApplicationRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalSecurityApplicationRepository.htm)
* [LocalSecurityDeviceRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalSecurityDeviceRepository.htm)
* [LocalSecurityPolicyRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalSecurityPolicyRepository.htm)
* [LocalSecurityRoleRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalSecurityRoleRepositoryService.htm)
* [LocalSecurityUserRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalSecurityUserRepositoryService.htm)
* [LocalTemplateDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalTemplateDefinitionRepositoryService.htm)
* [LocalOrganizationRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalOrganizationRepository.htm)
* [LocalPlaceRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalPlaceRepository.htm)
* [LocalUserEntityRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalUserEntityRepository.htm)
* [LocalConceptRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalConceptRepository.htm)