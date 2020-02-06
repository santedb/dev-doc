# Multi-Instance Mode

When leveraging SanteDB in multi-instance mode, the server will store local copies of data from source systems \(denoted by the device principal or the application principal on the current AuthenticationContext\). Each local system is permitted complete control over their local record \(as denoted by its provenance of the last version created\), or may attempt to update the master record which will result in the creation of a local record.

### Configuring Multi-Instance Mode

To enable multi-instance mode, you must:

1. Enable the MdmDataManagementService in the configuration
2. Enable an IRecordMatching service in your configuration \(so the MDM service can determine how to group together locals to a master\)
3. Configure the matching configurations you wish to use for each type of entity or act which should be used in MDM mode.

#### Enabling the Multi-Instance Data Management Service

To enable the daemon service MdmDataManagementService, add the daemon to your services configuration:

```markup
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="8">
    <serviceProviders>
      ...
      <add type="SanteDB.Persistence.MDM.Services.MdmDataManagementService, SanteDB.Persistence.MDM, Version=1.0.0.0"/>
    </serviceProviders>
</section>
```

#### Enabling an Record Matching Service

SanteDB allows the creation of custom IRecordMatchingService contracts, however it also provides both a deterministic and probabilistic matching engine. You can enable either by adding their daemon and a compatible IRecordMatchingConfigurationManager service to the services configuration:

```markup
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="8">
    <serviceProviders>
      ...
      <add type="SanteDB.Matcher.Matchers.ProbabalisticRecordMatchingService, SanteDB.Matcher, Version=1.0.0.0"/>
      <add type="SanteDB.Matcher.Configuration.File.FileMatchConfigurationProvider, SanteDB.Matcher.Configuration.File, Version=1.0.0.0"/>
    </serviceProviders>
</section>
```

If you're using the AppletConfigurationProvider you can place your matching configuration in any applet PAK file and it use it, if you're using the FileMatchConfigurationProvider you will have to configure the directories to monitor for match configuration

```markup
 <section xsi:type="FileMatchConfigurationSection">
    <basePath>
      <add readonly="false">C:\Users\fyfej\source\repos\santedb\sante-mpi\applet\matching</add>
      <add readonly="false">C:\Users\justin fyfe\source\repos\santedb\santempi\applet\matching</add>
    </basePath>
  </section>
```

{% hint style="info" %}
The FileMatchConfigurationProvider is great if you're running a debugging server or a server which allows users to create new match configurations as it will allow for the administration and re-load of match configurations in real time.
{% endhint %}

#### Configure Matching &lt;&gt; Resource Links

Both the single-instance-mode and multi-instance-mode persistence services leverage the ResourceMergeConfigurationSection to control how resources are matched and merged. You can configure the resources which are auto-matched and auto-merged by adding each resource type to the configuration section:

```markup
<section xsi:type="ResourceMergeConfigurationSection">
    <resources>
      <add type="Patient" matchConfiguration="org.santedb.smpi.matching.default" autoMerge="false" />
    </resources>
  </section>
```

