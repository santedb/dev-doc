---
description: IConceptRepositoryService (SanteDB.Core.Api)
---

# Concept Repository

## Summary

Represents a service which is responsible for the maintenance of concepts.

## Operations

| Operation                   | Response/Return       | Input/Parameter                                                                                   | Description                                                   |
| --------------------------- | --------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| FindConceptsByName          | IEnumerable\<Concept> | <p><em>String</em> <strong>name</strong><br><em>String</em> <strong>language</strong></p>         | Searches for a concept by name and language.                  |
| FindConceptsByReferenceTerm | IEnumerable\<Concept> | <p><em>String</em> <strong>code</strong><br><em>Uri</em> <strong>codeSystem</strong></p>          | Finds a concept by reference term.                            |
| GetConceptSetMembers        | IEnumerable\<Concept> | _String_ **mnemonic**                                                                             | Get concept set members                                       |
| FindConceptsByReferenceTerm | IEnumerable\<Concept> | <p><em>String</em> <strong>code</strong><br><em>String</em> <strong>codeSystemDomain</strong></p> | Finds a concept by reference term.                            |
| GetConcept                  | Concept               | _String_ **mnemonic**                                                                             | Gets a concept by mnemonic.                                   |
| Implies                     | Boolean               | <p><em>Concept</em> <strong>a</strong><br><em>Concept</em> <strong>b</strong></p>                 | Returns a value which indicates whether  implies              |
| IsMember                    | Boolean               | <p><em>ConceptSet</em> <strong>set</strong><br><em>Concept</em> <strong>concept</strong></p>      | Returns true if the concept  is a member of set               |
| IsMember                    | Boolean               | <p><em>Guid</em> <strong>set</strong><br><em>Guid</em> <strong>concept</strong></p>               | Returns true if the concept  is a member of set               |
| GetConceptReferenceTerm     | ReferenceTerm         | <p><em>Guid</em> <strong>conceptId</strong><br><em>String</em> <strong>codeSystem</strong></p>    | Gets the concept reference term for the specified code system |

## Implementations

### LocalConceptRepository - (SanteDB.Core)

Represents a service which is responsible for the maintenance of concepts.

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

## Example Implementation

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
    public IEnumerable<Concept> FindConceptsByReferenceTerm(String code,Uri codeSystem){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get concept set members
    /// </summary>
    public IEnumerable<Concept> GetConceptSetMembers(String mnemonic){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Finds a concept by reference term.
    /// </summary>
    public IEnumerable<Concept> FindConceptsByReferenceTerm(String code,String codeSystemDomain){
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
    public ReferenceTerm GetConceptReferenceTerm(Guid conceptId,String codeSystem){
        throw new System.NotImplementedException();
    }
}
```

## Usage Examples

### Lookup Reference Term From Concept

This example is particularly useful for those who are looking to convert an internal property (in the example GenderConcept) into a wire-level code system (in the example: HL7 v2 Administrative Sex).

```csharp
var conceptRepository = ApplicationServiceContext.Current.GetService<IConceptRepositoryService>();

// Map to HL7 Gender code
var hl7Code = conceptRepository.GetConceptReferenceTerm(patient.GenderConceptKey.GetValueOrDefault(), "1.3.6.1.4.1.33349.3.1.5.9.3.200.1");

// Map to FHIR Gender Code
var fhirCode = conceptRepository.GetConceptReferenceTerm(patient.GenderConceptKey.GetValueOrDefault(), "http://hl7.org/fhir/administrative-gender");
```

### Lookup Concept from Reference Term

This example illustrates using the concept repository to translate a wire-level code from HL7 FHIR to an internal concept.

```csharp
var conceptRepository = ApplicationServiceContext.Current.GetService<IConceptRepositoryService>();

// From FHIR simple coding
var genderConcept = conceptRepository.FindConceptsByReferenceTerm(resource.Gender.Value, "http://hl7.org/fhir/administrative-gender");

// From FHIR codeable concept
var coding = resource.MaritalStatus.Coding.First();
var marriageStatus = conceptRepository.FindConceptsByReferenceTerm(coding.Code.Value, coding.System);
```
