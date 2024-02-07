# Passive Services

In SanteDB, a passive service represents a service provider (implementation of a service contract) which is constructed and called on demand. These differ from daemon services as they are constructed on-demand.

Services available are listed in the [Service Definitions](../../../../server-plugins/implementing-.net-features/service-definitions/) wiki article. Writing and using a service involves:

1. Implementing the service contract interface
2. Registering the service with the ApplicationServiceHost
3. Calling the service / having your service called

## Implementing Service Contracts

### IServiceImplementation

All service interfaces also implement the `IServiceImplementation`. This interface contains a single property called `ServiceName` which is used in logs and configuration tooling to identify the service you've implemented to humans.&#x20;

For example, a simple service implementation of the barcode generator service would be:

```csharp
public class MyService : IBarcodeGeneratorService { 
    
    /// <summary>
    /// The name of the service
    /// </summary>
    public String ServiceName => "My own IBarcodeGeneratorService service";
    
    /// <summary>
    /// Generate a barcode from the specified identifier
    /// </summary>
    public Stream Generate<TEntity>(IEnumerable<IdentifierBase<TEntity>> identifers){
        // Do Stuff Here
    }
}
```

### ServiceProviderAttribute

You may also affix the `[ServiceProvider]` attribute to your service definition class in order to provide hints to the application context about your service's requirements.

The service provider attribute accepts these parameters:

| Parameter     | Type    | Use                                                                                                                                                                                                    |
| ------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Name          | String  | Override the ServiceName property                                                                                                                                                                      |
| Required      | Boolean | Indicates that the service should not be disabled by users from user interfaces.                                                                                                                       |
| Configuration | Type    | If your service uses an IConfigurationSection implementation to control configuration, this is the type of the configuration section the service uses. (NB: This is used by the configuration tooling) |
| Type          | Enum    | Indicates whether the service is a Singleton (only one instance is created during the entire SanteDB runtime) or PerCall (a service instance is created each time GetService is called)                |
| Dependencies  | Type\[] | An array of other service interfaces that must be running before this service starts.                                                                                                                  |

### Service Lifecycle

Services are constructed whenever they are first used by another subsystem in the SanteDB software stack. Services can be either singletons or instance per call.

#### Singleton Services

This is the default mode for passive service construction. Whenever a service is marked as a singleton the application context will construct a new instance of the service provider on startup, and will continue to use a single instance of the service provider for the lifetime of the application.

Services can be explicitly marked as singletons using the service provider attribute:

```csharp
[ServiceProvider(Name = "Singleton Service", Type = ServiceInstantiationType.Singleton)]
public class MyBarcodeGeneratorService : IBarcodeGeneratorService
{
    public MyBarcodeGeneratorService () {
        // Called once at application startup
    }
}
```

#### PerCall Services

Instance services are those services which are constructed on each call to `GetService<T>()` , this means that your service instances can use state variables, it also means that repeated calls to `GetService<T>` , will return different instances of the service.

```csharp
[ServiceProvider(Name = "Demand Instanced Service", Type = ServiceInstantiationType.PerCall)]
public class MyBarcodeGeneratorService : IBarcodeGeneratorService
{
    public MyBarcodeGeneratorService() {
    // Called every time GetService<T> is called
    }
}
```

{% hint style="warning" %}
Per-Call services are not currently not compatible with the Dependency Injection method of service calling. Only ApplicationServiceContext.GetService\<T>() calls adhere to Per-Call rule, DI uses of a Per-Call service are constructed once when the service using DI is constructed.

i.e. If ServiceA uses ServiceB via DI, and ServiceB is PerCall, then ServiceB is constructed once when ServiceA is constructed. If ServiceC uses ServiceB then a different instance of ServiceB is constructed for ServiceC's DI.
{% endhint %}
