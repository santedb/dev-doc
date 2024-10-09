`IValidatingRepositoryService&lt;TModel>` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a repository that can validate

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Validate|TModel|*TModel* **data**|Validates the supplied data and returns a valid copy (or) throws an appropriate exception|

# Implementations


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
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyValidatingRepositoryService<TModel> : SanteDB.Core.Services.IValidatingRepositoryService<TModel> { 
	public String ServiceName => "My own IValidatingRepositoryService`1 service";
	/// <summary>
	/// Validates the supplied data and returns a valid copy (or) throws an appropriate exception
	/// </summary>
	public TModel Validate(TModel data){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IValidatingRepositoryService&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IValidatingRepositoryService_1.htm)
* [GenericLocalActRepository&lt;TAct> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalActRepository_1.htm)
* [GenericLocalClinicalDataRepository&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalClinicalDataRepository_1.htm)
* [GenericLocalConceptRepository&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalConceptRepository_1.htm)
* [GenericLocalMetadataRepository&lt;TMetadata> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalMetadataRepository_1.htm)
* [GenericLocalRepository&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalRepository_1.htm)
* [GenericLocalRepositoryEx&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalRepositoryEx_1.htm)
* [GenericLocalSecurityRepository&lt;TSecurityEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_GenericLocalSecurityRepository_1.htm)
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
