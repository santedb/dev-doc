# Daemon Services

In SanteDB, a daemon service represents a service which is activated on startup and is shut down on service stop. Daemon services can exist on the iCDR and dCDR interfaces. Daemon services are implemented using the [`IDaemonService`](broken-reference)``

Daemons are particularly useful when:

* The plugin needs to subscribe to events on other services
* The plugin needs to register / configure other services on application start
* The plugin wants a long-running background task (like a messaging interface, listener, etc.)

### Lifecycle

Daemons go through the same lifecycle as the primary application host. Daemons have their `.Start()` method called at Stage 2 of the application startup and their `.Stop()` method called when the application host is shutting down.

## Implementation

### Daemon Scaffolding

Implementing the IDaemonService interface is all that is required to indicate a particular implementation is a daemon.

```csharp
public class HelloDaemon : IDaemonService
{

    public bool IsRunning => false;

    public string ServiceName => "HelloWorld Daemon";

    public event EventHandler Starting;
    public event EventHandler Started;
    public event EventHandler Stopping;
    public event EventHandler Stopped;

    public bool Start()
    {
        // Start the daemon
    }

    public bool Stop()
    {
        // Stop the daemon
    }
}
```

### Events

The IDaemonService implementation has four events which daemons are expected to raise. These events allow other modules/services to detect when your daemon has completed the necessary steps to start its services. For example, you may wish to have your daemon only start after a repository service is finished starting up, etc. The events are:

| Event    | Description                                                                                                                                         |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Starting | This event should be fired when your daemon has initiated its startup process.                                                                      |
| Started  | This event should be fired after your daemon service has completed all necessary startup processes.                                                 |
| Stopping | This event should be fired when your daemon has initiated shutdown. This allows other services to handle that your service(s) may not be available. |
| Stopped  | This event should be fired after your daemon has finished its shutdown process.                                                                     |

### Current Status

You should allow other services to detect whether your daemon has completed startup and is currently active. This state is indicated by the `IsRunning` property.

### Start/Stop Methods

The `Start()` method should, at minimum be implemented as:

```csharp
public bool Start() {
    // Notify of startup
    this.Starting?.Invoke(this, EventArgs.Empty);
    
    // Do your startup stuff here
    
    // Notify that startup has completed
    this.Started?.Invoke(this, EventArgs.Empty);
    
    // Finally, let the application host know you started up 
    return true;
}
```

The Stop() method is implemented in a similar manner:

```csharp
public bool Stop() {
    // Notify of stop
    this.Stopping?.Invoke(this, EventArgs.Empty);
    
    // Do your shutdown stuff
    
    // Notify that shutdown hsa stopped
    this.Stopped?.Invoke(this, EventArgs.Empty);
    
    // Finally let the application host know you shutdown properly
    return true;
}
```
