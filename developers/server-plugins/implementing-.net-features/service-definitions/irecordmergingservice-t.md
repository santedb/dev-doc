`IRecordMergingService&lt;T>` in assembly SanteDB.Core.Api version 3.0.1980.0

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


## SimResourceInterceptor&lt;TModel> - (SanteDB.Core.Api)
Single Instance Mode Handler
### Description
This class binds to startup and enables the listening and merging of records based on the record matcher
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## MdmEntityMerger&lt;TEntity> - (SanteDB.Persistence.MDM)
An MDM merger that operates on Entities
### Description
This class exists to allow callers to interact with the operations in the underlying infrastructure.
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## MdmResourceMerger&lt;TModel> - (SanteDB.Persistence.MDM)
An implementation of a IRecordMergeService for an MDM controlled resource
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}
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

* [IRecordMergingService&lt;T> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRecordMergingService_1.htm)
* [SimResourceInterceptor&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Management_SimResourceInterceptor_1.htm)
* [MdmEntityMerger&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmEntityMerger_1.htm)
* [MdmResourceMerger&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmResourceMerger_1.htm)
