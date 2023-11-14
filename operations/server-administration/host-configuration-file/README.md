# Server Configuration File

SanteDB dCDR and iCDR use a file-based configuration system to control the behaviors of the host process, synchronization, etc. Variables within the host configuration file are required to start up the core services of the SanteDB server.

The configuration options in the configuration file differ from those which control business behavior in that they are system settings. As such:

* Changes to the configuration file require a restart of the host process,
* Because changes require a restart - NO REST API may modify settings within the configuration file, since a REST API would be (in effect) controlling service uptime
  * The dCDR interfaces do allow minor modifications of configuration via web-interfaces.

## Structure

The overall configuration file structure is illustrated in the code block below:

```markup
<SanteDBConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       version="2.0.60.0" 
       xmlns:santempi="http://santedb.org/configuration/santempi" 
       xmlns:santeguard="http://santedb.org/configuration/santeguard" 
       xmlns="http://santedb.org/configuration">
       <sections>
              <!-- Section Registration -->
       </sections>
       <section xsi:type="SectionType">
       </section>
</SanteDBConfiguration>
```

{% hint style="info" %}
The SanteDB configuration files are identical in structure on the iCDR, dCDR (on Windows, Linux, Android, etc.). This commonality between platforms and frameworks is why SanteDB does not leverage the default .NET app.config or config.json structures.
{% endhint %}

The namespace definitions used in the configuration file allow plugins to isolate their configuration types. The default SanteDB configuration namespaces are:

| Solution     | Namespace                                   |
| ------------ | ------------------------------------------- |
| SanteDB Core | http://santedb.org/configuration            |
| SanteMPI     | http://santedb.org/configuration/santempi   |
| SanteGuard   | http://santedb.org/configuration/santeguard |

The configuration must contain two sections:

* Header - Which contains the \<sections> element and identifies to the configuration engine which IConfigurationSection instances are being used (see [Configuration Wiki Page](../../../developers/server-plugins/implementing-.net-features/configuration/))
* Configuration Sections - Which contain the \<section> element and configure the actual plugins in SanteDB.

## Sections Element

The \<sections> element identifies the types of IConfigurationSection you're deployment uses. The section element contains one or more \<add> elements with a type reference:

```markup
  <sections>
    <add type="SanteDB.Core.Configuration.DiagnosticsConfigurationSection, SanteDB.Core.Api, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.AppletConfigurationSection, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.ApplicationServiceContextConfigurationSection, SanteDB.Core.Api, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.Data.DataConfigurationSection, SanteDB.Core.Api, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Caching.Memory.Configuration.MemoryCacheConfigurationSection, SanteDB.Caching.Memory, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.RestConfigurationSection, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.ClaimsAuthorizationConfigurationSection, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.SecurityConfigurationSection, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Messaging.HDSI.Configuration.HdsiConfigurationSection, SanteDB.Messaging.HDSI, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Persistence.Data.ADO.Configuration.AdoPersistenceConfigurationSection, SanteDB.Persistence.Data.ADO, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.OrmLite.Configuration.OrmConfigurationSection, SanteDB.OrmLite, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.AuditAccountabilityConfigurationSection, SanteDB.Core.Api, Version=1.10.0.0"/>
```

At minimum, your configuration file should contain/use the following configuration sections documented on this section.

## Configuration Sections

* [DiagnosticsConfigurationSection](diagnostics-configuration.md)
* [AppletConfigurationSection](applet-configuration.md)
* [ApplicationServiceContextConfigurationSection](application-service-context-configuration.md)
* [DataConfigurationSection](data-configuration.md)
* MemoryCacheConfigurationSection
* RestConfigurationSection
* ClaimsAuthorizationConfigurationSection
* SecurityConfigurationSection
* HdsiConfigurationSection
* AdoPersistenceConfigurationSection
* OrmConfigurationSection
* AuditAccountabilityConfigurationSection

