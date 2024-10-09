`IRecordMergingService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Record merging service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetMergeCandidateKeys|IEnumerable&lt;Guid>|*Guid* **masterKey**|Gets the duplicates for the specified master record|
|GetMergeCandidates|IQueryResultSet&lt;IdentifiedData>|*Guid* **masterKey**|Get merge candidate keys|
|GetGlobalMergeCandidates|IQueryResultSet&lt;ITargetedAssociation>|*none*|TODO|
|GetIgnoredKeys|IEnumerable&lt;Guid>|*Guid* **masterKey**|Gets the ignore list for the specified master record|
|GetIgnored|IQueryResultSet&lt;IdentifiedData>|*Guid* **masterKey**|Gets the ignore list for the specified master record|
|Ignore|IdentifiedData|*Guid* **masterKey**<br/>*IEnumerable&lt;Guid>* **falsePositives**|Indicates that the engine should ignore the specified false positives|
|UnIgnore|IdentifiedData|*Guid* **masterKey**<br/>*IEnumerable&lt;Guid>* **ignoredKeys**|Indicates that an ignored record should be removed from the ignore list|
|Merge|RecordMergeResult|*Guid* **masterKey**<br/>*IEnumerable&lt;Guid>* **linkedDuplicates**|Merges the specified  into|
|Unmerge|RecordMergeResult|*Guid* **masterKey**<br/>*Guid* **unmergeDuplicateKey**|Un-merges the specified  from|
|DetectGlobalMergeCandidates|void|*none*|TODO|
|ClearGlobalMergeCanadidates|void|*none*|TODO|
|ClearGlobalIgnoreFlags|void|*none*|TODO|
|ClearMergeCandidates|void|*Guid* **masterKey**|Clear all merge candidates|
|ClearIgnoreFlags|void|*Guid* **masterKey**|Clear ignored flags|
|DetectMergeCandidates|void|*Guid* **masterKey**|Perform the necessary operations to detect merge candidates for|
|Reset|void|*Guid* **masterKey**<br/>*Boolean* **includeVerified**<br/>*Boolean* **linksOnly**|Reset the specified merge service data on the specified record|
|Reset|void|*Boolean* **includeVerified**<br/>*Boolean* **linksOnly**|Reset the specified merge service data on the specified record|

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
public class MyRecordMergingService : SanteDB.Core.Services.IRecordMergingService { 
	public String ServiceName => "My own IRecordMergingService service";
	/// <summary>
	/// Gets the duplicates for the specified master record
	/// </summary>
	public IEnumerable<Guid> GetMergeCandidateKeys(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get merge candidate keys
	/// </summary>
	public IQueryResultSet<IdentifiedData> GetMergeCandidates(Guid masterKey){
		throw new System.NotImplementedException();
	}
	public IQueryResultSet<ITargetedAssociation> GetGlobalMergeCandidates(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the ignore list for the specified master record
	/// </summary>
	public IEnumerable<Guid> GetIgnoredKeys(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the ignore list for the specified master record
	/// </summary>
	public IQueryResultSet<IdentifiedData> GetIgnored(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that the engine should ignore the specified false positives
	/// </summary>
	public IdentifiedData Ignore(Guid masterKey,IEnumerable<Guid> falsePositives){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that an ignored record should be removed from the ignore list
	/// </summary>
	public IdentifiedData UnIgnore(Guid masterKey,IEnumerable<Guid> ignoredKeys){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Merges the specified  into
	/// </summary>
	public RecordMergeResult Merge(Guid masterKey,IEnumerable<Guid> linkedDuplicates){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Un-merges the specified  from
	/// </summary>
	public RecordMergeResult Unmerge(Guid masterKey,Guid unmergeDuplicateKey){
		throw new System.NotImplementedException();
	}
	public void DetectGlobalMergeCandidates(){
		throw new System.NotImplementedException();
	}
	public void ClearGlobalMergeCanadidates(){
		throw new System.NotImplementedException();
	}
	public void ClearGlobalIgnoreFlags(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clear all merge candidates
	/// </summary>
	public void ClearMergeCandidates(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clear ignored flags
	/// </summary>
	public void ClearIgnoreFlags(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Perform the necessary operations to detect merge candidates for
	/// </summary>
	public void DetectMergeCandidates(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Reset the specified merge service data on the specified record
	/// </summary>
	public void Reset(Guid masterKey,Boolean includeVerified,Boolean linksOnly){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Reset the specified merge service data on the specified record
	/// </summary>
	public void Reset(Boolean includeVerified,Boolean linksOnly){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IRecordMergingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRecordMergingService.htm)
* [SimResourceInterceptor&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Management_SimResourceInterceptor_1.htm)
* [MdmEntityMerger&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmEntityMerger_1.htm)
* [MdmResourceMerger&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmResourceMerger_1.htm)
