# Application Service Context Configuration

The ApplicationServiceContextConfigurationSection section is used to control the [application context which acts as the service locator](../../../santedb/software-architecture/#service-architecture).&#x20;

```markup
<section xsi:type="ApplicationServiceContextConfigurationSection" 
  threadPoolSize="8">
    <serviceProviders>
      <add type="SanteDB.Core.Services.Impl.FileConfigurationService, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
      <!-- Repeat for each service definition -->
    </serviceProviders>
  </section>
```

The @threadPoolSize attribute controls the number of reserved threads created in the application's default thread pool. The thread pool is used to overcome the expense of spinning up operating system threads on request, and is useful for limiting the CPU use of the server (with the understanding that additional clients will need to wait in a queue).

Each of the \<add> elements in the \<serviceProviders> element identifies the service class registration that should be loaded and used in the iCDR or dCDR.
