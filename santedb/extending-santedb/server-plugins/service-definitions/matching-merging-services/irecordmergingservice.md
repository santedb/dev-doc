---
description: IRecordMergingService<T> (SanteDB.Core.Api)
---

# Record Merging Service

## Summary

Represents a service which appropriately merges / unmerges records

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Merging | EventHandler&lt;DataMergingEventArgs&lt;T&gt;&gt; | Fired prior to a merge occurring |
| Merged | EventHandler&lt;DataMergeEventArgs&lt;T&gt;&gt; | Fired after a merge has occurred |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| GetDuplicates | IEnumerable&lt;T&gt; | _Guid_ **masterKey** | Gets the duplicates for the specified master record |
| GetIgnored | IEnumerable&lt;T&gt; | _Guid_ **masterKey** | Gets the ignore list for the specified master record |
| Ignore | T | _Guid_ **masterKey** _IEnumerable&lt;Guid&gt;_ **falsePositives** | Indicates that the engine should ignore the specified false positives |
| UnIgnore | T | _Guid_ **masterKey** _IEnumerable&lt;Guid&gt;_ **ignoredKeys** | Indicates that an ignored record should be removed from the ignore list |
| Merge | T | _Guid_ **masterKey** _IEnumerable&lt;Guid&gt;_ **linkedDuplicates** | Merges the specified  into |
| Unmerge | T | _Guid_ **masterKey** _Guid_ **unmergeDuplicateKey** | Un-merges the specified  from |
| Diff | Patch | _Guid_ **masterKey** _Guid_ **linkedDuplicateKey** | Gets the differences between the master and the linked duplicate |
| FlagDuplicates | void | _String_ **configurationName** | Clears all candidates and re-runs the specified  for the entire database |
| FlagDuplicates | T | _Guid_ **key** _String_ **configurationName** | Clears all candidates and re-runs the specified  for the entire database |

## Implementations

None

## Example Implementation

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

