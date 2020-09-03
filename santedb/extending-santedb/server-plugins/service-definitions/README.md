# Service Definitions

Whenever you write a plugin for SanteDB, you are actually implementing and consuming a series of service contracts. Whenever another plugin wants a particular service it will ask the host context for the currently configured service instance and call the relevant method on the contract.

Alternately, when you wish to call a service you must ask for the current contract. For example, if you wanted to search for a patient , you would call:

```csharp
var repo = ApplicationServiceContext.Current.GetService<IRepositoryService<Patient>>();
var patients = repo.Find(p=>p.Identifiers.Any(i=>i.Value == "102938293"));
```

This code instructs the service host to retrieve the currently configured patient repository \(whether it is a database, HTTP call, a link to a shared health record\) and execute the specified query.

### 

