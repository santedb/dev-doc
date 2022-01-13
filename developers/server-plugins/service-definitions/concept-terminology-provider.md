Concept/Terminology Provider (IConceptRepositoryService in SanteDB.Core.Api)

# Summary
Represents a service which is responsible for the maintenance of concepts.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindConceptsByName|IEnumerable&lt;Concept>|*String* **name**<br/>*String* **language**|Searches for a concept by name and language.|
|FindConceptsByReferenceTerm|IEnumerable&lt;ConceptReferenceTerm>|*String* **code**<br/>*Uri* **codeSystem**|Finds a concept by reference term.|
|GetConceptSetMembers|IEnumerable&lt;Concept>|*String* **mnemonic**|Get concept set members|
|GetConceptByReferenceTerm|Concept|*String* **code**<br/>*String* **codeSystemDomain**|Finds a concept by reference term only where the concept is equivalent|
|FindConceptsByReferenceTerm|IEnumerable&lt;ConceptReferenceTerm>|*String* **code**<br/>*String* **codeSystemDomain**|Finds a concept by reference term.|
|GetConcept|Concept|*String* **mnemonic**|Gets a concept by mnemonic.|
|Implies|Boolean|*Concept* **a**<br/>*Concept* **b**|Returns a value which indicates whether  implies|
|IsMember|Boolean|*ConceptSet* **set**<br/>*Concept* **concept**|Returns true if the concept  is a member of set|
|IsMember|Boolean|*Guid* **set**<br/>*Guid* **concept**|Returns true if the concept  is a member of set|
|GetConceptReferenceTerm|ReferenceTerm|*Guid* **conceptId**<br/>*String* **codeSystem**<br/>*Boolean* **exact**|Gets the concept reference term for the specified code system|
|GetConceptReferenceTerm|ReferenceTerm|*String* **conceptMnemonic**<br/>*String* **codeSystem**|Gets the concept reference term for the specified code system|
|FindReferenceTermsByConcept|IEnumerable&lt;ConceptReferenceTerm>|*Guid* **conceptId**<br/>*String* **codeSystem**|Gets the concept reference term for the specified code system|

# Implementations


## LocalConceptRepository - (SanteDB.Server.Core)
Represents a service which is responsible for the
            maintenance of concepts.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalConceptRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyConceptRepositoryService : SanteDB.Core.Services.IConceptRepositoryService { 
	public String ServiceName => "My own IConceptRepositoryService service";
	/// <summary>
	/// Searches for a concept by name and language.
	/// </summary>
	public IEnumerable<Concept> FindConceptsByName(String name,String language){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds a concept by reference term.
	/// </summary>
	public IEnumerable<ConceptReferenceTerm> FindConceptsByReferenceTerm(String code,Uri codeSystem){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get concept set members
	/// </summary>
	public IEnumerable<Concept> GetConceptSetMembers(String mnemonic){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds a concept by reference term only where the concept is equivalent
	/// </summary>
	public Concept GetConceptByReferenceTerm(String code,String codeSystemDomain){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds a concept by reference term.
	/// </summary>
	public IEnumerable<ConceptReferenceTerm> FindConceptsByReferenceTerm(String code,String codeSystemDomain){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets a concept by mnemonic.
	/// </summary>
	public Concept GetConcept(String mnemonic){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns a value which indicates whether  implies
	/// </summary>
	public Boolean Implies(Concept a,Concept b){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the concept  is a member of set
	/// </summary>
	public Boolean IsMember(ConceptSet set,Concept concept){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the concept  is a member of set
	/// </summary>
	public Boolean IsMember(Guid set,Guid concept){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the concept reference term for the specified code system
	/// </summary>
	public ReferenceTerm GetConceptReferenceTerm(Guid conceptId,String codeSystem,Boolean exact){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the concept reference term for the specified code system
	/// </summary>
	public ReferenceTerm GetConceptReferenceTerm(String conceptMnemonic,String codeSystem){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the concept reference term for the specified code system
	/// </summary>
	public IEnumerable<ConceptReferenceTerm> FindReferenceTermsByConcept(Guid conceptId,String codeSystem){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IConceptRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IConceptRepositoryService.htm)
* [LocalConceptRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalConceptRepository.htm)
