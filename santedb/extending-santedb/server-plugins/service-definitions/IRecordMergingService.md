---
description: IRecordMergingService`1 (SanteDB.Core.Api)
---

## Summary
Represents a service which appropriately merges / unmerges records

## Events

|Event|Type|Description|
|-|-|-|
|Merging|System.EventHandler&lt;SanteDB.Core.Event.DataMergingEventArgs&lt;T>>|Fired prior to a merge occurring|
|Merged|System.EventHandler&lt;SanteDB.Core.Event.DataMergeEventArgs&lt;T>>|Fired after a merge has occurred|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetDuplicates|System.Collections.Generic.IEnumerable&lt;T>|masterKey <small style='border:solid 1px #aaa'>System.Guid</small>|Gets the duplicates for the specified master record|
|GetIgnored|System.Collections.Generic.IEnumerable&lt;T>|masterKey <small style='border:solid 1px #aaa'>System.Guid</small>|Gets the ignore list for the specified master record|
|Ignore|T|masterKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>falsePositives <small style='border:solid 1px #aaa'>System.Collections.Generic.IEnumerable<System.Guid></small>|Indicates that the engine should ignore the specified false positives|
|UnIgnore|T|masterKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>ignoredKeys <small style='border:solid 1px #aaa'>System.Collections.Generic.IEnumerable<System.Guid></small>|Indicates that an ignored record should be removed from the ignore list|
|Merge|T|masterKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>linkedDuplicates <small style='border:solid 1px #aaa'>System.Collections.Generic.IEnumerable<System.Guid></small>|Merges the specified  into|
|Unmerge|T|masterKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>unmergeDuplicateKey <small style='border:solid 1px #aaa'>System.Guid</small>|Un-merges the specified  from|
|Diff|SanteDB.Core.Model.Patch.Patch|masterKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>linkedDuplicateKey <small style='border:solid 1px #aaa'>System.Guid</small>|Gets the differences between the master and the linked duplicate|
|FlagDuplicates|void|configurationName <small style='border:solid 1px #aaa'>System.String</small>|Clears all candidates and re-runs the specified  for the entire database|
|FlagDuplicates|T|key <small style='border:solid 1px #aaa'>System.Guid</small><br/>configurationName <small style='border:solid 1px #aaa'>System.String</small>|Clears all candidates and re-runs the specified  for the entire database|

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
	public event System.EventHandler<SanteDB.Core.Event.DataMergingEventArgs<T>> Merging;
	/// <summary>
	/// Fired after a merge has occurred
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataMergeEventArgs<T>> Merged;
	/// <summary>
	/// Gets the duplicates for the specified master record
	/// </summary>
	public System.Collections.Generic.IEnumerable<T> GetDuplicates(System.Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the ignore list for the specified master record
	/// </summary>
	public System.Collections.Generic.IEnumerable<T> GetIgnored(System.Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that the engine should ignore the specified false positives
	/// </summary>
	public T Ignore(System.Guid masterKey,System.Collections.Generic.IEnumerable<System.Guid> falsePositives){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that an ignored record should be removed from the ignore list
	/// </summary>
	public T UnIgnore(System.Guid masterKey,System.Collections.Generic.IEnumerable<System.Guid> ignoredKeys){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Merges the specified  into
	/// </summary>
	public T Merge(System.Guid masterKey,System.Collections.Generic.IEnumerable<System.Guid> linkedDuplicates){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Un-merges the specified  from
	/// </summary>
	public T Unmerge(System.Guid masterKey,System.Guid unmergeDuplicateKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the differences between the master and the linked duplicate
	/// </summary>
	public SanteDB.Core.Model.Patch.Patch Diff(System.Guid masterKey,System.Guid linkedDuplicateKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clears all candidates and re-runs the specified  for the entire database
	/// </summary>
	public void FlagDuplicates(System.String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clears all candidates and re-runs the specified  for the entire database
	/// </summary>
	public T FlagDuplicates(System.Guid key,System.String configurationName){
		throw new System.NotImplementedException();
	}
}
```
