---
description: IBusinessRulesService`1 (SanteDB.Core.Api)
---

## Summary
Represents a service that executes business rules based on triggers which happen in the persistence layer

### Remarks
Note: This can be done, instead with events on the persistence layer on the SanteDB datalayer, however there
            may come a time when a rule is fired without persistence occurring

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyBusinessRulesService<TModel> : SanteDB.Core.Services.IBusinessRulesService<TModel> { 
	public String ServiceName => "My own IBusinessRulesService`1 service";
	/// <summary>
	/// Gets or sets the rule to be run after this rule (for chained rules)
	/// </summary>
	public SanteDB.Core.Services.IBusinessRulesService<TModel> Next {
		get;
		set;
	}
	/// <summary>
	/// Called after an insert occurs
	/// </summary>
	public TModel AfterInsert(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after obsolete committed
	/// </summary>
	public TModel AfterObsolete(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after query
	/// </summary>
	public System.Collections.Generic.IEnumerable<TModel> AfterQuery(System.Collections.Generic.IEnumerable<TModel> results){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after retrieve
	/// </summary>
	public TModel AfterRetrieve(TModel result){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after update committed
	/// </summary>
	public TModel AfterUpdate(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called before an insert occurs
	/// </summary>
	public TModel BeforeInsert(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called before obsolete
	/// </summary>
	public TModel BeforeObsolete(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called before an update occurs
	/// </summary>
	public TModel BeforeUpdate(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called to validate a specific object
	/// </summary>
	public System.Collections.Generic.List<SanteDB.Core.BusinessRules.DetectedIssue> Validate(TModel data){
		throw new System.NotImplementedException();
	}
}
```
