---
description: IRecordMatchingService (SanteDB.Core.Api)
---

## Summary
Represents a service that performs record matching and classification

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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRecordMatchingService : SanteDB.Core.Services.IRecordMatchingService { 
	public String ServiceName => "My own IRecordMatchingService service";
	/// <summary>
	/// Instructs the record matching service to perform a quick block function of records            for type  with
	/// </summary>
	public System.Collections.Generic.IEnumerable<T> Block<T>(T input,System.String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the record matcher to run a detailed classification on the matching blocks in
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Services.IRecordMatchResult<T>> Classify<T>(T input,System.Collections.Generic.IEnumerable<T> blocks,System.String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the record matcher to run a block and match operation against
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Services.IRecordMatchResult<T>> Match<T>(T input,System.String configurationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Performs a score against the specified query (how confident the match is that the  matches the
	/// </summary>
	public SanteDB.Core.Services.IRecordMatchResult<T> Score<T>(T input,System.Linq.Expressions.Expression<System.Func<T,System.Boolean>> query,System.String configurationName){
		throw new System.NotImplementedException();
	}
}
```