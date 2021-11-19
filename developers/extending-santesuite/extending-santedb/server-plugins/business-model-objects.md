# Business Model Objects

Objects in the SanteDB.Model package represent the core business model objects. These objects are responsible for representing the logical information model as a series of C# classes. These classes:

* Contain minimal serialization metadata which allow SanteDB data to be serialized and parsed to/from JSON or XML in the synchronization format.
* Contain basic behaviors (described here) which allow for utility such determining equality, deep-cloning, and copying.&#x20;
* Tools for delay loading chained properties (for example loading GenderConcept from the keyed concept)

## Delay Loading Property Values

By default, the primary properties on any object loaded from the database on initial query. These are any simple values like UUIDs, strings, etc. and are loaded when the core object is loaded.&#x20;

Take, for example a Patient object loaded from the database.

```csharp
var patientRepository = ApplicationServiceContext.Current.GetService<IRepositoryService<Patient>>();
var patient = patientRepository.Find(p=>p.Identifiers.Any(id=>id.Value == "TEST")).FirstOrDefault();

// Simple properties are loaded
Console.WriteLine("Gender: {0}", patient.GenderConceptKey);
// Output: Gender: UUID HERE

// Related Properties cannot be accessed 
// Throws null reference exception
Console.WriteLine("Gender Mnemonic: {0}", patient.GenderConcept.Mnemonic);
```

You can opt to fetch the GenderConcept using the `IRepositoryService<Concept>` service, or, you can use the shortcut method `.LoadProperty()` method.

```csharp
Console.WriteLine("Gender Mnemonic: {0}", patient.LoadProperty(o=>o.GenderConcept).Mnemonic);
// Output: MALE
```

The operations for delay loading are. These properties are loaded using the EntitySourceProvider.

| Function                             | Example                                              |
| ------------------------------------ | ---------------------------------------------------- |
| `.LoadProperty(o=>o.PropertyName)`   | `.LoadProperty(o=>o.GenderConcept).Mnemonic`         |
| `.LoadCollection(o=>o.PropertyName)` | `.LoadProperty(o=>o.Names).FirstOrDefault()`         |
| `.LoadProperty<T>(PropertyName)`     | `.LoadProperty<Concept>("GenderConcept").Mnemonic`   |
| `.LoadCollection<T>(PropertyName)`   | `.LoadProperty<EntityName>("Name").FirstOrDefault()` |

