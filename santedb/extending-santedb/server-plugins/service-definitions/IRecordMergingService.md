---
description: IRecordMergingService<T> (SanteDB.Core.Api)
---

## Summary
Represents a service which appropriately merges / unmerges records

## Events

|Event|Type|Description|
|-|-|-|
|Merging|EventHandler&lt;DataMergingEventArgs&lt;T>>|Fired prior to a merge occurring|
|Merged|EventHandler&lt;DataMergeEventArgs&lt;T>>|Fired after a merge has occurred|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetDuplicates|IEnumerable&lt;T>|*Guid* **masterKey**|Gets the duplicates for the specified master record|
|GetIgnored|IEnumerable&lt;T>|*Guid* **masterKey**|Gets the ignore list for the specified master record|
|Ignore|T|*Guid* **masterKey**<br/>*IEnumerable<Guid>* **falsePositives**|Indicates that the engine should ignore the specified false positives|
|UnIgnore|T|*Guid* **masterKey**<br/>*IEnumerable<Guid>* **ignoredKeys**|Indicates that an ignored record should be removed from the ignore list|
|Merge|T|*Guid* **masterKey**<br/>*IEnumerable<Guid>* **linkedDuplicates**|Merges the specified  into|
|Unmerge|T|*Guid* **masterKey**<br/>*Guid* **unmergeDuplicateKey**|Un-merges the specified  from|
|Diff|Patch|*Guid* **masterKey**<br/>*Guid* **linkedDuplicateKey**|Gets the differences between the master and the linked duplicate|
|FlagDuplicates|void|*String* **configurationName**|Clears all candidates and re-runs the specified  for the entire database|
|FlagDuplicates|T|*Guid* **key**<br/>*String* **configurationName**|Clears all candidates and re-runs the specified  for the entire database|

## Implementations

None

## Example
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
	/// Gets the duplicates for the specified master record
	/// </summary>
	public IEnumerable<T> GetDuplicates(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the ignore list for the specified master record
	/// </summary>
	public IEnumerable<T> GetIgnored(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that the engine should ignore the specified false positives
	/// </summary>
	public T Ignore(Guid masterKey,IEnumerable<Guid> falsePositives){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that an ignored record should be removed from the ignore list
	/// </summary>
	public T UnIgnore(Guid masterKey,IEnumerable<Guid> ignoredKeys){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Merges the specified  into
	/// </summary>
	public T Merge(Guid masterKey,IEnumerable<Guid> linkedDuplicates){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Un-merges the specified  from
	/// </summary>
	public T Unmerge(Guid masterKey,Guid unmergeDuplicateKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the differences between the master and the linked duplicate
	/// </summary>
	public Patch Diff(Guid masterKey,Guid linkedDuplicateKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clears all candidates and re-runs the specified  for the entire database
	/// </summary>
	public void FlagDuplicates(String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clears all candidates and re-runs the specified  for the entire database
	/// </summary>
	public T FlagDuplicates(Guid key,String configurationName){
		throw new System.NotImplementedException();
	}
}
```
