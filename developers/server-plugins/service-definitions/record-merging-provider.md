Record Merging Provider (IRecordMergingService in SanteDB.Core.Api)

# Summary
Record merging service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetMergeCandidateKeys|IEnumerable&lt;Guid>|*Guid* **masterKey**|Gets the duplicates for the specified master record|
|GetMergeCandidates|IEnumerable&lt;IdentifiedData>|*Guid* **masterKey**|Get merge candidate keys|
|GetGlobalMergeCandidates|IEnumerable&lt;ITargetedAssociation>|*Int32* **count**<br/>*Int32* **offset**<br/>*Int32&* **totalResults**|Get all merge candidates|
|GetIgnoredKeys|IEnumerable&lt;Guid>|*Guid* **masterKey**|Gets the ignore list for the specified master record|
|GetIgnored|IEnumerable&lt;IdentifiedData>|*Guid* **masterKey**|Gets the ignore list for the specified master record|
|Ignore|IdentifiedData|*Guid* **masterKey**<br/>*IEnumerable&lt;Guid>* **falsePositives**|Indicates that the engine should ignore the specified false positives|
|UnIgnore|IdentifiedData|*Guid* **masterKey**<br/>*IEnumerable&lt;Guid>* **ignoredKeys**|Indicates that an ignored record should be removed from the ignore list|
|Merge|RecordMergeResult|*Guid* **masterKey**<br/>*IEnumerable&lt;Guid>* **linkedDuplicates**|Merges the specified  into|
|Unmerge|RecordMergeResult|*Guid* **masterKey**<br/>*Guid* **unmergeDuplicateKey**|Un-merges the specified  from|
|DetectGlobalMergeCandidates|void||TODO|
|ClearGlobalMergeCanadidates|void||TODO|
|ClearGlobalIgnoreFlags|void||TODO|
|ClearMergeCandidates|void|*Guid* **masterKey**|Clear all merge candidates|
|ClearIgnoreFlags|void|*Guid* **masterKey**|Clear ignored flags|
|Reset|void|*Guid* **masterKey**<br/>*Boolean* **includeVerified**<br/>*Boolean* **linksOnly**|Reset the specified merge service data on the specified record|
|Reset|void|*Boolean* **includeVerified**<br/>*Boolean* **linksOnly**|Reset the specified merge service data on the specified record|

# Implementations


## SimResourceMerger&lt;TModel> - (SanteDB.Core.Api)
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

## MdmEntityMerger&lt;TEntity> - (SanteDB.Persistence.MDM)
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

## MdmResourceMerger&lt;TModel> - (SanteDB.Persistence.MDM)
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
	public IEnumerable<IdentifiedData> GetMergeCandidates(Guid masterKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all merge candidates
	/// </summary>
	public IEnumerable<ITargetedAssociation> GetGlobalMergeCandidates(Int32 count,Int32 offset,Int32& totalResults){
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
	public IEnumerable<IdentifiedData> GetIgnored(Guid masterKey){
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
* [SimResourceMerger&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_SimDataManagementService+SimResourceMerger_1.htm)
* [MdmEntityMerger&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmEntityMerger_1.htm)
* [MdmResourceMerger&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_Resources_MdmResourceMerger_1.htm)
