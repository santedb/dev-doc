# Service Definitions

Whenever you write a plugin for SanteDB, you are actually implementing and consuming a series of service contracts. Whenever another plugin wants a particular service it will ask the host context for the currently configured service instance and call the relevant method on the contract.

Alternately, when you wish to call a service you must ask for the current contract. For example, if you wanted to search for a patient , you would call:

```csharp
var repo = ApplicationServiceContext.Current.GetService<IRepositoryService<Patient>>();
var patients = repo.Find(p=>p.Identifiers.Any(i=>i.Value == "102938293"));
```

This code instructs the service host to retrieve the currently configured patient repository \(whether it is a database, HTTP call, a link to a shared health record\) and execute the specified query.

### IServiceImplementation

All service interfaces also implement the IServiceImplementation. This interface contains a single property called _ServiceName_ which is used in logs and configuration tooling to identify the service you've implemented to humans \(aka meat computers\).

### ServiceProviderAttribute

Additionally, your service may be annotated with the ServiceProviderAttribute attribute. This provider attribute allows for declarative dependency indication, trace logging, etc.

The service provider attribute accepts these parameters:

| Parameter | Type | Use |
| :--- | :--- | :--- |
| Name | String | Override the ServiceName property |
| Required | Boolean | Indicates that the service should not be disabled by users from user interfaces. |
| Configuration | Type | If your service uses an IConfigurationSection implementation to control configuration, this is the type of the configuration section the service uses. \(NB: This is used by the configuration tooling\) |
| Type | Enum | Indicates whether the service is a Singleton \(only one instance is created during the entire SnateDB runtime\) or PerCall \(a service instance is created each time GetService is called\) |
| Dependencies | Type\[\] | An array of other service interfaces that must be running before this service starts. |

### 

