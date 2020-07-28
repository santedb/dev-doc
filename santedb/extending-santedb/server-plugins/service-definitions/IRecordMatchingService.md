---
description: IRecordMatchingService (SanteDB.Core.Api)
---

## Summary
Represents a service that performs record matching and classification

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Block|IEnumerable&lt;T>|*T* **input**<br/>*String* **configurationName**|Instructs the record matching service to perform a quick block function of records            for type  with|
|Classify|IEnumerable&lt;IRecordMatchResult&lt;T>>|*T* **input**<br/>*IEnumerable&lt;T>* **blocks**<br/>*String* **configurationName**|Instructs the record matcher to run a detailed classification on the matching blocks in|
|Match|IEnumerable&lt;IRecordMatchResult&lt;T>>|*T* **input**<br/>*String* **configurationName**|Instructs the record matcher to run a block and match operation against|
|Score|IRecordMatchResult&lt;T>|*T* **input**<br/>*Expression&lt;Func&lt;T,Boolean>>* **query**<br/>*String* **configurationName**|Performs a score against the specified query (how confident the match is that the  matches the|

## Implementations


### SanteMatch Deterministic Matcher - (SanteDB.Matcher)
Represents a deterministic record matching service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Matchers.SimpleRecordMatchingService, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### SanteMatch Probabalistic Match Service - (SanteDB.Matcher)
Represents a probabalistic record matching service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Matchers.WeightedRecordMatchingService, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRecordMatchingService : SanteDB.Core.Services.IRecordMatchingService { 
	public String ServiceName => "My own IRecordMatchingService service";
	/// <summary>
	/// Instructs the record matching service to perform a quick block function of records            for type  with
	/// </summary>
	public IEnumerable<T> Block<T>(T input,String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the record matcher to run a detailed classification on the matching blocks in
	/// </summary>
	public IEnumerable<IRecordMatchResult<T>> Classify<T>(T input,IEnumerable<T> blocks,String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the record matcher to run a block and match operation against
	/// </summary>
	public IEnumerable<IRecordMatchResult<T>> Match<T>(T input,String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Performs a score against the specified query (how confident the match is that the  matches the
	/// </summary>
	public IRecordMatchResult<T> Score<T>(T input,Expression<Func<T,Boolean>> query,String configurationName){
		throw new System.NotImplementedException();
	}
}
```
