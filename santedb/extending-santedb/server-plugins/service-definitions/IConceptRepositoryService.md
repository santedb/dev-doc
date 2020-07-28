---
description: IConceptRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service which is responsible for the maintenance of concepts.

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindConceptsByName|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.DataTypes.Concept>|name <small style='border:solid 1px #aaa'>System.String</small><br/>language <small style='border:solid 1px #aaa'>System.String</small>|Searches for a concept by name and language.|
|FindConceptsByReferenceTerm|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.DataTypes.Concept>|code <small style='border:solid 1px #aaa'>System.String</small><br/>codeSystem <small style='border:solid 1px #aaa'>System.Uri</small>|Finds a concept by reference term.|
|GetConceptSetMembers|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.DataTypes.Concept>|mnemonic <small style='border:solid 1px #aaa'>System.String</small>|Get concept set members|
|FindConceptsByReferenceTerm|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.DataTypes.Concept>|code <small style='border:solid 1px #aaa'>System.String</small><br/>codeSystemDomain <small style='border:solid 1px #aaa'>System.String</small>|Finds a concept by reference term.|
|GetConcept|SanteDB.Core.Model.DataTypes.Concept|mnemonic <small style='border:solid 1px #aaa'>System.String</small>|Gets a concept by mnemonic.|
|Implies|System.Boolean|a <small style='border:solid 1px #aaa'>SanteDB.Core.Model.DataTypes.Concept</small><br/>b <small style='border:solid 1px #aaa'>SanteDB.Core.Model.DataTypes.Concept</small>|Returns a value which indicates whether  implies|
|IsMember|System.Boolean|set <small style='border:solid 1px #aaa'>SanteDB.Core.Model.DataTypes.ConceptSet</small><br/>concept <small style='border:solid 1px #aaa'>SanteDB.Core.Model.DataTypes.Concept</small>|Returns true if the concept  is a member of set|
|IsMember|System.Boolean|set <small style='border:solid 1px #aaa'>System.Guid</small><br/>concept <small style='border:solid 1px #aaa'>System.Guid</small>|Returns true if the concept  is a member of set|
|GetConceptReferenceTerm|SanteDB.Core.Model.DataTypes.ReferenceTerm|conceptId <small style='border:solid 1px #aaa'>System.Guid</small><br/>codeSystem <small style='border:solid 1px #aaa'>System.String</small>|Gets the concept reference term for the specified code system|

## Implementations


### LocalConceptRepository - (SanteDB.Core)
Represents a service which is responsible for the
            maintenance of concepts.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalConceptRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyConceptRepositoryService : SanteDB.Core.Services.IConceptRepositoryService { 
	public String ServiceName => "My own IConceptRepositoryService service";
	/// <summary>
	/// Searches for a concept by name and language.
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.DataTypes.Concept> FindConceptsByName(System.String name,System.String language){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds a concept by reference term.
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.DataTypes.Concept> FindConceptsByReferenceTerm(System.String code,System.Uri codeSystem){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get concept set members
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.DataTypes.Concept> GetConceptSetMembers(System.String mnemonic){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds a concept by reference term.
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.DataTypes.Concept> FindConceptsByReferenceTerm(System.String code,System.String codeSystemDomain){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets a concept by mnemonic.
	/// </summary>
	public SanteDB.Core.Model.DataTypes.Concept GetConcept(System.String mnemonic){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns a value which indicates whether  implies
	/// </summary>
	public System.Boolean Implies(SanteDB.Core.Model.DataTypes.Concept a,SanteDB.Core.Model.DataTypes.Concept b){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the concept  is a member of set
	/// </summary>
	public System.Boolean IsMember(SanteDB.Core.Model.DataTypes.ConceptSet set,SanteDB.Core.Model.DataTypes.Concept concept){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the concept  is a member of set
	/// </summary>
	public System.Boolean IsMember(System.Guid set,System.Guid concept){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the concept reference term for the specified code system
	/// </summary>
	public SanteDB.Core.Model.DataTypes.ReferenceTerm GetConceptReferenceTerm(System.Guid conceptId,System.String codeSystem){
		throw new System.NotImplementedException();
	}
}
```
