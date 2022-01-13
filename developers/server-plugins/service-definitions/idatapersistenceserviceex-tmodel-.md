---
description: IDataPersistenceServiceEx`1 (IDataPersistenceServiceEx<TModel> in SanteDB.Core.Api)
---

# Summary
Generic interface implementation

# Implementations


## ActPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service which persists ACT classes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ActPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptPersistenceService - (SanteDB.Persistence.Data.ADO)
Concept persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ConceptPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityPersistenceService - (SanteDB.Persistence.Data.ADO)
Entity persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## VersionedDataPersistenceService`3 - (SanteDB.Persistence.Data.ADO)
Versioned domain data

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.VersionedDataPersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataPersistenceServiceEx<TModel> : SanteDB.Core.Services.IDataPersistenceServiceEx<TModel> { 
	public String ServiceName => "My own IDataPersistenceServiceEx`1 service";
}
```

# References

* [IDataPersistenceServiceEx`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceServiceEx`1.htm)
* [ActPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ActPersistenceService.htm)
* [ConceptPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ConceptPersistenceService.htm)
* [EntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityPersistenceService.htm)
* [VersionedDataPersistenceService`3 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_VersionedDataPersistenceService`3.htm)
