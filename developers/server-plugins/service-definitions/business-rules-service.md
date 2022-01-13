`IBusinessRulesService&lt;TModel>` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a service that executes business rules based on triggers which happen in the [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) layer

## Description
When a business rules implementation is attached to the service context, or via the ```AddBusinessRule``` method,
            the SanteDB server call the appropiate Before/After functions on the implementation, before checking the ```Next``` property
            to follow the next business rule in the chain.

The [JavaScript Business Rules Engine](https://help.santesuite.org/developers/applets/business-rules) which loads
            data from installed applets is an example of an implementation of this service which translates events into Javascript callbacks. Implementers can use
            this service to:

* Generate unique identifiers or other data and affix it to data
* Intercept queries and write requests and perform re-writes
* Log, catalog, or update external indexes of data
* Cancel or interrupt the default flow of a persistence or query operation


Note: This can be done, instead with events on the persistence layer on the SanteDB datalayer, however there
            may come a time when a rule is fired without persistence occurring

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Next|IBusinessRulesService&lt;TModel>|RW|Gets or sets the rule to be run after this rule (for chained rules)|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|AfterInsert|TModel|*TModel* **data**|Called after an insert occurs.|
|AfterObsolete|TModel|*TModel* **data**|Called after obsolete has been committed|
|AfterQuery|IEnumerable&lt;TModel>|*IEnumerable&lt;TModel>* **results**|Called after a query has been executed|
|AfterRetrieve|TModel|*TModel* **result**|Called after retrieve of an object|
|AfterUpdate|TModel|*TModel* **data**|Called after update has been committed|
|BeforeInsert|TModel|*TModel* **data**|Called before an insert occurs|
|BeforeObsolete|TModel|*TModel* **data**|Called before obsolete occurs|
|BeforeUpdate|TModel|*TModel* **data**|Called before an update occurs|
|Validate|List&lt;DetectedIssue>|*TModel* **data**|Called to validate the data provided|

# Implementations


## JavascriptBusinessRule&lt;TBinding> - (SanteDB.BusinessRules.JavaScript)
Wrapper for [IBusinessRulesService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBusinessRulesService.htm) which calls one or more JavaScript functions
### Description
This implementation of the business rules wrapper is used to interface with business rules written in 
            [SanteDB's JavaScript Business Rules Engine](https://help.santesuite.org/developers/applets/business-rules) and allows 
            implementers to customize the behavior of the iCDR or dCDR with JavaScript within their applets. Whenever a call to the ```SanteDBBre.AddBusinessRule()```
            interface is called from applet initialization, a new instance of this class is chained into the execution pipeline. From there, the events raised
            for before/after insert/update/obsolete/query are translated to JavaScript and the provided callback is executed.

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
A business rule for [Bundle](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Collection_Bundle.htm) instances which performs a look-ahead on bundles
### Description
Whenever a [Bundle](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Collection_Bundle.htm) is submitted for processing to a SanteDB iCDR or dCDR server, 
            it is important that any JavaScript based business rules for object WITHIN the bundle are executed. However,
            we don't want to implement this in JavaScript itself since, everytime a bundle is sent to the server, 
            the entire bundle would be prepared (in JSON), passed to the JavaScript [JavascriptEngineBridge](http://santesuite.org/assets/doc/net/html/T_SanteDB_BusinessRules_JavaScript_JNI_JavascriptEngineBridge.htm) and then 
            parsed back out *regardless* of whether there were any rules or not

This business rule prevents this behavior by performing a look-ahead. It will scan the incoming bundle's objects
            to determine whether a JavaScript based business rule has been registered for the item, if it has, it will then 
            serialize the bundle, and call the appropriate rule for each object.

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

## BaseBusinessRulesService&lt;TModel> - (SanteDB.Core.Api)
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
Business rule that calls other [DataQualityBusinessRule`1](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityBusinessRule_1.htm) based on the contents of a bundle
### Description
This business rule wraps the insertion or update of a [Bundle](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Collection_Bundle.htm) and calls individual data quality validation 
            rules for each of the objects contained withing the bundle provided.

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

## DataQualityBusinessRule&lt;TModel> - (SanteDB.Core.Api)
A business rule that applies user defined data quality rules from the [IDataQualityConfigurationProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_IDataQualityConfigurationProviderService.htm)
### Description
This business rule template allows users to describe data quality rules (for example, using [the application configuration for data quality rules](https://help.santesuite.org/operations/server-administration/host-configuration-file/data-quality-services#configuring-data-quality-rules)) 
            to be applied to incoming data. This service uses the data quality extension to then flag any warnings or informational issues (error issues result in the object being rejected). 
            These extensions are cleaned by the [DataQualityExtensionCleanJob](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityExtensionCleanJob.htm) if the object no longer fails the quality rules.

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
	/// Called after an insert occurs.
	/// </summary>
	public TModel AfterInsert(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after obsolete has been committed
	/// </summary>
	public TModel AfterObsolete(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after a query has been executed
	/// </summary>
	public IEnumerable<TModel> AfterQuery(IEnumerable<TModel> results){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after retrieve of an object
	/// </summary>
	public TModel AfterRetrieve(TModel result){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Called after update has been committed
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
	/// Called before obsolete occurs
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
	/// Called to validate the data provided
	/// </summary>
	public List<DetectedIssue> Validate(TModel data){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBusinessRulesService&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBusinessRulesService_1.htm)
* [JavascriptBusinessRule&lt;TBinding> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BusinessRules_JavaScript_JavascriptBusinessRule_1.htm)
* [BundleWrapperRule C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BusinessRules_JavaScript_Rules_BundleWrapperRule.htm)
* [BaseBusinessRulesService&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_BaseBusinessRulesService_1.htm)
* [DataQualityBundleRule C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityBundleRule.htm)
* [DataQualityBusinessRule&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityBusinessRule_1.htm)
