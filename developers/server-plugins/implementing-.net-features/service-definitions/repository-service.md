`IRepositoryService&lt;TModel>` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a repository service

## Description
In the [SanteDB Software Architecture](https://help.santesuite.org/santedb/software-architecture#repository-services) the repository service 
            layer is the layer responsible for coordinating business rules, privacy, auditing, and other activities from the messaging or other 
            services in the SanteDB iCDR or dCDR.

Repository services should be the primary method of interacting with the SanteDB server infrastructure, as it indicates a user, application or
            device process is not intending to modify underlying persistence data directly (as would be the case for a system process), rather it wishes SanteDB
            to execute all validation and rules as normal.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|TModel|*Guid* **key**|Gets the specified model data|
|Get|TModel|*Guid* **key**<br/>*Guid* **versionKey**|Gets the specified model data|
|Find|IQueryResultSet&lt;TModel>|*Expression&lt;Func&lt;TModel,Boolean>>* **query**|Finds the specified data where the current version matches the query provided|
|Insert|TModel|*TModel* **data**|Inserts the specified model information|
|Save|TModel|*TModel* **data**|Inserts or updates the specified data|
|Delete|TModel|*Guid* **key**|Delete the object according to the current  or             according to server configuration|

# Implementations


## AmiUpstreamRepository&lt;TModel> - (SanteDB.Client)
HDSI upstream repository
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## AmiWrappedUpstreamRepository&lt;TModel,TWrapper> - (SanteDB.Client)
Wrapped upstream repository for AMI which uses the ISecurityEntityWrapper
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## HdsiUpstreamRepository&lt;TModel> - (SanteDB.Client)
HDSI upstream repository
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## UpstreamAuditRepository - (SanteDB.Client)
An upstream audit repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Repositories.UpstreamAuditRepository, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UpstreamRepositoryServiceBase&lt;TModel,TWireFormat,TCollection> - (SanteDB.Client)
A generic implementation that calls the upstream for fetching data
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## UpstreamForeignDataManagement - (SanteDB.Client)
Upstream foreign data management classes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Management.UpstreamForeignDataManagement, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalMailMessageService - (SanteDB.Core.Api)
Represents a [IMailMessageService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IMailMessageService.htm) which uses database persistence layer 
            to store / retrieve mail messages within the system

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalMailMessageService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericLocalActRepository&lt;TAct> - (SanteDB.Core.Api)
Represents an act repository service.
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericLocalClinicalDataRepository&lt;TModel> - (SanteDB.Core.Api)
Represents generic local clinical data repository
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericLocalConceptRepository&lt;TModel> - (SanteDB.Core.Api)
Generic local concept repository with sufficient permissions
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericLocalMetadataRepository&lt;TMetadata> - (SanteDB.Core.Api)
Provides generic basis for metadata editing
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## Local Repository Service - (SanteDB.Core.Api)
Represents a base class for entity repository services
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericLocalRepositoryEx&lt;TModel> - (SanteDB.Core.Api)
Generic nullifiable local repository
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericLocalSecurityRepository&lt;TSecurityEntity> - (SanteDB.Core.Api)
Generic local security repository
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## Default Audit Repository - (SanteDB.Core.Api)
Represents an audit repository which stores and queries audit data.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalAuditRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalBatchRepository - (SanteDB.Core.Api)
Local batch repository service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalBatchRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalCarePathwayDefinitionRepositoryService - (SanteDB.Core.Api)
Local care pathway definition

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalCarePathwayDefinitionRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalConceptRepository - (SanteDB.Core.Api)
Represents a service which is responsible for the maintenance of concepts using local persistence.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalConceptRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalContainerRepository - (SanteDB.Core.Api)
Place repository that uses local persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalContainerRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalEntityRelationshipRepository - (SanteDB.Core.Api)
Represents a local entity relationship repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalEntityRelationshipRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalEntityRepository - (SanteDB.Core.Api)
Local entity repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalEntityRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalExtensionTypeRepository - (SanteDB.Core.Api)
Local extension types

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalExtensionTypeRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalIdentityDomainRepository - (SanteDB.Core.Api)
Represents a repository service for managing assigning authorities.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalIdentityDomainRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalManufacturedMaterialRepository - (SanteDB.Core.Api)
Local material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalManufacturedMaterialRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalMaterialRepository - (SanteDB.Core.Api)
Local material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalMaterialRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalOrganizationRepository - (SanteDB.Core.Api)
Provides operations for managing organizations.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalOrganizationRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalPatientRepository - (SanteDB.Core.Api)
Local material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalPatientRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalPlaceRepository - (SanteDB.Core.Api)
Place repository that uses local persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalPlaceRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalProtocolRepositoryService - (SanteDB.Core.Api)
Default protocol repository services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalProtocolRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalProviderRepository - (SanteDB.Core.Api)
Provides operations for managing organizations.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalProviderRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityApplicationRepository - (SanteDB.Core.Api)
Local security application repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalSecurityApplicationRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityDeviceRepository - (SanteDB.Core.Api)
Local security device repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalSecurityDeviceRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityPolicyRepository - (SanteDB.Core.Api)
Alter policies

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalSecurityPolicyRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityRoleRepositoryService - (SanteDB.Core.Api)
Represents a local security role service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalSecurityRoleRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalSecurityUserRepositoryService - (SanteDB.Core.Api)
Security user repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalSecurityUserRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalTemplateDefinitionRepositoryService - (SanteDB.Core.Api)
Represents a local metadata repository service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalTemplateDefinitionRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LocalUserEntityRepository - (SanteDB.Core.Api)
Localuser entity repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalUserEntityRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AppletForeignDataMapRepository - (SanteDB.Core.Applets)
Applet foreign data map repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletForeignDataMapRepository, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AppletSubscriptionRepository - (SanteDB.Core.Applets)
An implementation of the [ISubscriptionRepository](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionRepository.htm) that loads definitions from applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletSubscriptionRepository, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MdmEntityRelationshipPersistenceProvider - (SanteDB.Persistence.MDM)
Relationship persistence provider passed through to underlying types

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.Resources.MdmEntityRelationshipPersistenceProvider, SanteDB.Persistence.MDM, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	/// Gets the specified model data
	/// </summary>
	public TModel Get(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified model data
	/// </summary>
	public TModel Get(Guid key,Guid versionKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data where the current version matches the query provided
	/// </summary>
	public IQueryResultSet<TModel> Find(Expression<Func<TModel,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts the specified model information
	/// </summary>
	public TModel Insert(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts or updates the specified data
	/// </summary>
	public TModel Save(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete the object according to the current  or             according to server configuration
	/// </summary>
	public TModel Delete(Guid key){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IRepositoryService&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService_1.htm)
* [AmiUpstreamRepository&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_AmiUpstreamRepository_1.htm)
* [AmiWrappedUpstreamRepository&lt;TModel,TWrapper> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_AmiWrappedUpstreamRepository_2.htm)
* [HdsiUpstreamRepository&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_HdsiUpstreamRepository_1.htm)
* [UpstreamAuditRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_UpstreamAuditRepository.htm)
* [UpstreamRepositoryServiceBase&lt;TModel,TWireFormat,TCollection> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_UpstreamRepositoryServiceBase_3.htm)
* [UpstreamForeignDataManagement C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Management_UpstreamForeignDataManagement.htm)
* [LocalMailMessageService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_LocalMailMessageService.htm)
* [GenericLocalActRepository&lt;TAct> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalActRepository_1.htm)
* [GenericLocalClinicalDataRepository&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalClinicalDataRepository_1.htm)
* [GenericLocalConceptRepository&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalConceptRepository_1.htm)
* [GenericLocalMetadataRepository&lt;TMetadata> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalMetadataRepository_1.htm)
* [GenericLocalRepository&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalRepository_1.htm)
* [GenericLocalRepositoryEx&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalRepositoryEx_1.htm)
* [GenericLocalSecurityRepository&lt;TSecurityEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalSecurityRepository_1.htm)
* [LocalAuditRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalAuditRepository.htm)
* [LocalBatchRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalBatchRepository.htm)
* [LocalCarePathwayDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalCarePathwayDefinitionRepositoryService.htm)
* [LocalConceptRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalConceptRepository.htm)
* [LocalContainerRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalContainerRepository.htm)
* [LocalEntityRelationshipRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalEntityRelationshipRepository.htm)
* [LocalEntityRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalEntityRepository.htm)
* [LocalExtensionTypeRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalExtensionTypeRepository.htm)
* [LocalIdentityDomainRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalIdentityDomainRepository.htm)
* [LocalManufacturedMaterialRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalManufacturedMaterialRepository.htm)
* [LocalMaterialRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalMaterialRepository.htm)
* [LocalOrganizationRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalOrganizationRepository.htm)
* [LocalPatientRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalPatientRepository.htm)
* [LocalPlaceRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalPlaceRepository.htm)
* [LocalProtocolRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalProtocolRepositoryService.htm)
* [LocalProviderRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalProviderRepository.htm)
* [LocalSecurityApplicationRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalSecurityApplicationRepository.htm)
* [LocalSecurityDeviceRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalSecurityDeviceRepository.htm)
* [LocalSecurityPolicyRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalSecurityPolicyRepository.htm)
* [LocalSecurityRoleRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalSecurityRoleRepositoryService.htm)
* [LocalSecurityUserRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalSecurityUserRepositoryService.htm)
* [LocalTemplateDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalTemplateDefinitionRepositoryService.htm)
* [LocalUserEntityRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalUserEntityRepository.htm)
* [AppletForeignDataMapRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletForeignDataMapRepository.htm)
* [AppletSubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletSubscriptionRepository.htm)
* [MdmEntityRelationshipPersistenceProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmEntityRelationshipPersistenceProvider.htm)
