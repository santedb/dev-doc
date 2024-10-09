`IRelationshipValidationProvider` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a class which can manage the valid relationship types between two objects

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetValidRelationships|IEnumerable&lt;RelationshipValidationRule>|*none*|Get all valid relationship types between  and all targets|
|GetValidRelationships|IEnumerable&lt;RelationshipValidationRule>|*Guid* **sourceClassKey**|Get all valid relationship types between  and all targets|
|QueryRelationships|IQueryResultSet&lt;RelationshipValidationRule>|*Expression&lt;Func&lt;RelationshipValidationRule,Boolean>>* **query**|Query for all relationships registered|
|AddValidRelationship|RelationshipValidationRule|*Nullable&lt;Guid>* **sourceClassKey**<br/>*Nullable&lt;Guid>* **targetClassKey**<br/>*Guid* **relationshipTypeKey**<br/>*String* **description**|Add a valid relationship between  and|
|RemoveValidRelationship|void|*Nullable&lt;Guid>* **sourceClassKey**<br/>*Nullable&lt;Guid>* **targetClassKey**<br/>*Guid* **relationshipTypeKey**|Remove the valid relationship type key between|
|GetRuleByKey|RelationshipValidationRule|*Guid* **key**|Get a relationship directly using the key of the relationship.|
|RemoveRuleByKey|RelationshipValidationRule|*Guid* **key**|Remove a relationship directly using the key of the relationship.|

# Implementations


## AdoRelationshipValidationProvider - (SanteDB.Persistence.Data)
ADO.NET Based Relationship Provider
### Description
This class allows for the management of validation rules between entities, 
            acts, or entities and acts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoRelationshipValidationProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRelationshipValidationProvider : SanteDB.Core.Services.IRelationshipValidationProvider { 
	public String ServiceName => "My own IRelationshipValidationProvider service";
	/// <summary>
	/// Get all valid relationship types between  and all targets
	/// </summary>
	public IEnumerable<RelationshipValidationRule> GetValidRelationships<TRelationship>(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all valid relationship types between  and all targets
	/// </summary>
	public IEnumerable<RelationshipValidationRule> GetValidRelationships<TRelationship>(Guid sourceClassKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query for all relationships registered
	/// </summary>
	public IQueryResultSet<RelationshipValidationRule> QueryRelationships(Expression<Func<RelationshipValidationRule,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a valid relationship between  and
	/// </summary>
	public RelationshipValidationRule AddValidRelationship<TRelationship>(Nullable<Guid> sourceClassKey,Nullable<Guid> targetClassKey,Guid relationshipTypeKey,String description){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove the valid relationship type key between
	/// </summary>
	public void RemoveValidRelationship<TRelationship>(Nullable<Guid> sourceClassKey,Nullable<Guid> targetClassKey,Guid relationshipTypeKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a relationship directly using the key of the relationship.
	/// </summary>
	public RelationshipValidationRule GetRuleByKey(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove a relationship directly using the key of the relationship.
	/// </summary>
	public RelationshipValidationRule RemoveRuleByKey(Guid key){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IRelationshipValidationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRelationshipValidationProvider.htm)
* [AdoRelationshipValidationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoRelationshipValidationProvider.htm)
