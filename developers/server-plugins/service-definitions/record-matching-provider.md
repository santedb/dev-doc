`IRecordMatchingService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a service that performs record matching and classification

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Block|IEnumerable&lt;T>|*T* **input**<br/>*String* **configurationId**<br/>*IEnumerable&lt;Guid>* **ignoreList**<br/>*IRecordMatchingDiagnosticSession* **collector**|Instructs the record matching service to perform a quick block function of records            for type  with|
|Classify|IEnumerable&lt;IRecordMatchResult&lt;T>>|*T* **input**<br/>*IEnumerable&lt;T>* **blocks**<br/>*String* **configurationId**<br/>*IRecordMatchingDiagnosticSession* **collector**|Instructs the record matcher to run a detailed classification on the matching blocks in|
|Match|IEnumerable&lt;IRecordMatchResult&lt;T>>|*T* **input**<br/>*String* **configurationId**<br/>*IEnumerable&lt;Guid>* **ignoreList**<br/>*IRecordMatchingDiagnosticSession* **collector**|Instructs the record matcher to run a block and match operation against|
|Match|IEnumerable&lt;IRecordMatchResult>|*IdentifiedData* **input**<br/>*String* **configurationId**<br/>*IEnumerable&lt;Guid>* **ignoreList**<br/>*IRecordMatchingDiagnosticSession* **collector**|A non-generic method which uses the type of  to call Match<T>|
|Classify|IEnumerable&lt;IRecordMatchResult>|*IdentifiedData* **input**<br/>*IEnumerable&lt;IdentifiedData>* **blocks**<br/>*String* **configurationId**<br/>*IRecordMatchingDiagnosticSession* **collector**|A non-generic method which uses the type of  to call Classify<T>|
|CreateDiagnosticSession|IRecordMatchingDiagnosticSession|*none*|TODO|

# Implementations


## BaseRecordMatchingService - (SanteDB.Matcher)
Represents base record matching service for SanteDB Matcher
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## SanteMatch Deterministic Matcher - (SanteDB.Matcher)
Represents a deterministic record matching service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Matchers.SimpleRecordMatchingService, SanteDB.Matcher, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SanteMatch Probabalistic Match Service - (SanteDB.Matcher)
Represents a probabalistic record matching service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Matchers.WeightedRecordMatchingService, SanteDB.Matcher, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MdmRecordMatchingService - (SanteDB.Persistence.MDM)
Represents a matching service that wraps the underlying system
            IRecordMatchingService and provides additional functionality

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.MdmRecordMatchingService, SanteDB.Persistence.MDM, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Matching;
/// Other usings here
public class MyRecordMatchingService : SanteDB.Core.Matching.IRecordMatchingService { 
	public String ServiceName => "My own IRecordMatchingService service";
	/// <summary>
	/// Instructs the record matching service to perform a quick block function of records            for type  with
	/// </summary>
	public IEnumerable<T> Block<T>(T input,String configurationId,IEnumerable<Guid> ignoreList,IRecordMatchingDiagnosticSession collector){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the record matcher to run a detailed classification on the matching blocks in
	/// </summary>
	public IEnumerable<IRecordMatchResult<T>> Classify<T>(T input,IEnumerable<T> blocks,String configurationId,IRecordMatchingDiagnosticSession collector){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the record matcher to run a block and match operation against
	/// </summary>
	public IEnumerable<IRecordMatchResult<T>> Match<T>(T input,String configurationId,IEnumerable<Guid> ignoreList,IRecordMatchingDiagnosticSession collector){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// A non-generic method which uses the type of  to call Match<T>
	/// </summary>
	public IEnumerable<IRecordMatchResult> Match(IdentifiedData input,String configurationId,IEnumerable<Guid> ignoreList,IRecordMatchingDiagnosticSession collector){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// A non-generic method which uses the type of  to call Classify<T>
	/// </summary>
	public IEnumerable<IRecordMatchResult> Classify(IdentifiedData input,IEnumerable<IdentifiedData> blocks,String configurationId,IRecordMatchingDiagnosticSession collector){
		throw new System.NotImplementedException();
	}
	public IRecordMatchingDiagnosticSession CreateDiagnosticSession(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IRecordMatchingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Matching_IRecordMatchingService.htm)
* [BaseRecordMatchingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Matcher_Matchers_BaseRecordMatchingService.htm)
* [SimpleRecordMatchingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Matcher_Matchers_SimpleRecordMatchingService.htm)
* [WeightedRecordMatchingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Matcher_Matchers_WeightedRecordMatchingService.htm)
* [MdmRecordMatchingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_MdmRecordMatchingService.htm)
