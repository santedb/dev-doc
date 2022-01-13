---
description: IBusinessRulesService`1 (IBusinessRulesService<TModel> in SanteDB.Core.Api)
---

# Summary
Represents a service that executes business rules based on triggers which happen in the persistence layer

## Description
Note: This can be done, instead with events on the persistence layer on the SanteDB datalayer, however there
            may come a time when a rule is fired without persistence occurring

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Next|IBusinessRulesService&lt;TModel>|RW|Gets or sets the rule to be run after this rule (for chained rules)|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AfterInsert|TModel|*TModel* **data**|Called after an insert occurs|
|AfterObsolete|TModel|*TModel* **data**|Called after obsolete committed|
|AfterQuery|IEnumerable&lt;TModel>|*IEnumerable&lt;TModel>* **results**|Called after query|
|AfterRetrieve|TModel|*TModel* **result**|Called after retrieve|
|AfterUpdate|TModel|*TModel* **data**|Called after update committed|
|BeforeInsert|TModel|*TModel* **data**|Called before an insert occurs|
|BeforeObsolete|TModel|*TModel* **data**|Called before obsolete|
|BeforeUpdate|TModel|*TModel* **data**|Called before an update occurs|
|Validate|List&lt;DetectedIssue>|*TModel* **data**|Called to validate a specific object|

# Implementations


## JavascriptBusinessRule`1 - (SanteDB.BusinessRules.JavaScript)
Represents a rule service base binding

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BusinessRules.JavaScript.JavascriptBusinessRule`1, SanteDB.BusinessRules.JavaScript, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## BundleWrapperRule - (SanteDB.BusinessRules.JavaScript)
Represents a rule which is tied JavaScript which executes a bundle

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BusinessRules.JavaScript.Rules.BundleWrapperRule, SanteDB.BusinessRules.JavaScript, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## BaseBusinessRulesService`1 - (SanteDB.Core.Api)
Represents a business rules service with no behavior, but intended to help in the implementation of another
            business rules service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.BaseBusinessRulesService`1, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DataQualityBundleRule - (SanteDB.Core.Api)
Represents a bundle data quality rule

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Quality.DataQualityBundleRule, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DataQualityBusinessRule`1 - (SanteDB.Core.Api)
Represents a single data quality business rule

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Quality.DataQualityBusinessRule`1, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyBusinessRulesService<TModel> : SanteDB.Core.Services.IBusinessRulesService<TModel> { 
	public String ServiceName => "My own IBusinessRulesService`1 service";
	/// <summary>
	/// Gets or sets the rule to be run after this rule (for chained rules)
	/// </summary>
	public IBusinessRulesService<TModel> Next {
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
	public IEnumerable<TModel> AfterQuery(IEnumerable<TModel> results){
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
	public List<DetectedIssue> Validate(TModel data){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBusinessRulesService`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBusinessRulesService`1.htm)
* [JavascriptBusinessRule`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BusinessRules_JavaScript_JavascriptBusinessRule`1.htm)
* [BundleWrapperRule C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BusinessRules_JavaScript_Rules_BundleWrapperRule.htm)
* [BaseBusinessRulesService`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_BaseBusinessRulesService`1.htm)
* [DataQualityBundleRule C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityBundleRule.htm)
* [DataQualityBusinessRule`1 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityBusinessRule`1.htm)
