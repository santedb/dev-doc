# SanteDB Host Context

As described in the [Software Architecture](../../../../santedb/architecture/software-architecture.md#service-architecture) documentation, the SanteDB services or iCDR and dCDR leverage dependency injection and service locator patterns. In the iCDR and dCDR both of these patterns are managed by the `ApplicationServiceContext` instance.&#x20;

The implementation of `ApplicationServiceContext` depends on the environment that SanteDB is running within, they can be:

* Testing Context -> Used by the .NET unit testing framework&#x20;
* Server Context -> Used by the iCDR server application
* Configuration Context -> Used by the configuration tooling&#x20;
* Dc Context -> Used by the dCDR applications
* Mini Context -> Used by the applet debugger in the SDK

## Application Service Context Lifecycle

When the application context is initialized, it will go through a defined lifecycle, illustrated below:

![](<../../../../.gitbook/assets/image (403).png>)

### Startup

Before the host context becomes active, it first undergoes a startup procedure. This is a three stage process.

{% hint style="info" %}
During startup or in the case startup was unsuccessful, all requests to SanteDB will result in an `HTTP 503 Service Unavailable` result.&#x20;
{% endhint %}

#### Startup Stage 1 : Configuration and Preparation

In stage 1 of the startup the application host loads the base `IConfigurationProvider` service instance and instructs it to load its configuration files. It also loads the dependency injection manager and any configured plugins in the configuration file (including validation of the services listed in the `ApplicationServiceContextConfigurationSection` section).

#### Startup Stage 2 : Daemon Startup

In stage 2 of the startup procedure, the application context host scans the configuration for all `IDaemonService` implementations and calls the `Start()` method on those services. The daemon services are started in the order they appear in the configuration file.&#x20;

To implement a daemon service see [Implementing Daemon Services ](implementing-.net-features/daemon-services.md).

#### Startup Stage 3: Notify Start

In the final stage of startup, the `ApplicationServiceContext` will fire the `Started` event. Many plugins use this event to perform any last-minute binding or startup procedures. This is done because, by stage 3, the application host context has initialized its plugins and is, for all intents and purposes, running.

You can bind your service implementation to perform actions at stage 3 of startup by subscribing to the `Start` event:

```csharp
public class MyService : IServiceImplementation
{
    private ILocalizationService m_localeService;
    
    public MyService(ILocalizationService localeService) {
        this.m_localeService = localeService;
        // We want to wait until startup to bind to another service
        ApplicationServiceContext.Current.Started += (o,e) => {
            foreach(var s in this.m_localeService.GetStrings()) {
                // Do something now that the app context is loaded 
            }
        }
    }
```

### Shut Down

The shutdown procedure on SanteDB allows services and plugins to notify other systems of a shutdown, dispose of any unmanaged resources, and perform any garbage collection.

#### Shutdown Stage 1 : Daemon Stop

In stage 1 of the shutdown procedure the application context will notify all `IDaemonServices` of its shutdown using the `Stop()` method on the daemon. The daemons should perform any shutdown/stop procedures to remove themselves from the application domain context.

#### Shutdown Stage 2 : Dispose

In stage 2 shutdown, any services registered with the application context host which implement `IDisposable` will have their `Dispose()` method called. This allows any passie services to clean up unmanaged handles, and perform disposal of ports/bindings/etc.

{% hint style="info" %}
Knowledge of when and how to use`IDisposable` is considered background information. Consult [Microsoft's Documentation ](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable?view=net-5.0)for more information on when/how to use and implement `IDisposable`.&#x20;
{% endhint %}
