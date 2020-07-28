---
description: IConceptRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a service which is responsible for the maintenance of concepts.

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
