# Service Definitions

Whenever you write a plugin for SanteDB, you are actually implementing and consuming a series of service contracts. Whenever another plugin wants a particular service it will ask the host context for the currently configured service instance and call the relevant method on the contract.

Alternately, when you wish to call a service you must ask for the current implementation. There are two methods to do this:

* Service Locator Pattern ([https://en.wikipedia.org/wiki/Service\_locator\_pattern](https://en.wikipedia.org/wiki/Service\_locator\_pattern)) - Whereby service instances are located at runtime
* Dependency Injection Pattern ([https://en.wikipedia.org/wiki/Dependency\_injection](https://en.wikipedia.org/wiki/Dependency\_injection)) - Whereby services instances are injected into the class when constructed.

### Service Locator

You should use the service locator pattern when:

* Your plugin needs to operate on SanteDB iCDR and dCDR versions < 2.0.76
* Your plugin is going to use dynamic services (like IDataPersistenceService<> and IRepositoryService<>) where the services are registered at runtime.

Using the service locator pattern, your extension should:

* Get the current instance of the `ApplicationServiceContext.Current` class
* Call the `GetService<T>()` method passing the contract to the method
* Verify the service was registered by doing a null check.

Consider a service which finds a patient.

```csharp
public interface IPatientFinderService : IServiceImplementation {
     Patient FindPatient(string id);
}

public class PatientFinderProvider : IPatientFinderService {
     
     public string Name => "My Extended Service";
     
     public Patient FindPatient(string id) {
          // Get the repository service
          var repo = ApplicationServiceContext.Current.GetService<IRepositoryService<Patient>>();
          // Check if repository was null
          if(repo == null)
              throw new InvalidOperationException("Couldn't find a valid Patient Repository");
         
          // Return the patient
          return repo.Find(p=>p.Identifiers.Any(i=>i.Value == id)).FirstOrDefault();
     }
     
}
```

### Dependency Injection

Dependency injection was introduced in SanteDB 2.0.76 , you can use dependency injection when:

* Your plugin is targeting SanteDB iCDR > 2.0.76
* The services being injected are configured services not registered at runtime (i.e. they aren't dynamically generated)

Dependency injection is driven off the constructor, rules for this are:

* Your object should not define a default constructor (the DI code will assume you're using Service Locator instead)
* Should identify the required services using the service contract definition
* Should identify option services using a default value of null

Using our example from above, let's imagine we want to extend our class to cache the located result and to hash the identifier in the cache. Since the hashing and caching services are defined statically in the configuration file, we can use DI for this.

```csharp
public class PatientFinderProvider : IPatientFinderService {
     
     public string Name => "My Extended Service";
     
     // Add: Local references to static services
     private IAdHocCacheService adhocCache;
     private IPasswordHashingService hashingService;
     
     // Constructor indicating services required
     public PatientFinderProvider(IAdHocCacheService adHocCache, IPasswordHashingService hashingService)
     {
          this.adhocCache = adHocCache;
          this.hashingService = hashingService;
     }
     
     public Patient FindPatient(string id) {
     
          // Get the repository service
          var repo = ApplicationServiceContext.Current.GetService<IRepositoryService<Patient>>();
          // Check if repository was null
          if(repo == null)
              throw new InvalidOperationException("Couldn't find a valid Patient Repository");
         
          // Check if the patient exists in the cache
          var key = this.hashingService.ComputeHash(id);
          var patient = this.adhocCache.Get<Patient>(key);
          if(patient == null) // Load from DB
          {
               patient = repo.Find(p=>p.Identifiers.Any(i=>i.Value == id)).FirstOrDefault();
               this.adhocCache.Add(key, patient);
          }
          return patient;
     }
     
}
```

