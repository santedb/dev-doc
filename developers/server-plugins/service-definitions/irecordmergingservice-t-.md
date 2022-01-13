---
description: IRecordMergingService`1 (IRecordMergingService<T> in SanteDB.Core.Api)
---

# Summary
Represents a service which appropriately merges / unmerges records

# Events

|Event|Type|Description|
|-|-|-|
|Merging|EventHandler&lt;DataMergingEventArgs&lt;T>>|Fired prior to a merge occurring|
|Merged|EventHandler&lt;DataMergeEventArgs&lt;T>>|Fired after a merge has occurred|
|UnMerging|EventHandler&lt;DataMergingEventArgs&lt;T>>|Fired prior to a merge occurring|
|UnMerged|EventHandler&lt;DataMergeEventArgs&lt;T>>|Fired after a merge has occurred|

# Implementations


## SimResourceMerger`1 - (SanteDB.Core.Api)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.SimDataManagementService+SimResourceMerger`1, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MdmEntityMerger`1 - (SanteDB.Persistence.MDM)
An MDM merger that operates on Entities
### Description
This class exists to allow callers to interact with the operations in the underlying infrastructure.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.Resources.MdmEntityMerger`1, SanteDB.Persistence.MDM, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MdmResourceMerger`1 - (SanteDB.Persistence.MDM)
An implementation of a IRecordMergeService for an MDM controlled resource

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.Resources.MdmResourceMerger`1, SanteDB.Persistence.MDM, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRecordMergingService<T> : SanteDB.Core.Services.IRecordMergingService<T> { 
	public String ServiceName => "My own IRecordMergingService`1 service";
	/// <summary>
	/// Fired prior to a merge occurring
	/// </summary>
	public event EventHandler<DataMergingEventArgs<T>> Merging;
	/// <summary>
	/// Fired after a merge has occurred
	/// </summary>
	public event EventHandler<DataMergeEventArgs<T>> Merged;
	/// <summary>
	/// Fired prior to a merge occurring
	/// </summary>
	public event EventHandler<DataMergingEventArgs<T>> UnMerging;
	/// <summary>
	/// Fired after a merge has occurred
	/// </summary>
	public event EventHandler<DataMergeEventArgs<T>> UnMerged;
}
```

# References

* [IRecordMergingService`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRecordMergingService`1.htm)
* [SimResourceMerger`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_SimDataManagementService+SimResourceMerger`1.htm)
* [MdmEntityMerger`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmEntityMerger`1.htm)
* [MdmResourceMerger`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmResourceMerger`1.htm)
