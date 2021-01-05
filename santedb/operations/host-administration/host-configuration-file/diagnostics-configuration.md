# Diagnostics Configuration

The DiagnosticsConfigurationSection controls the logging and error reporting infrastructure. 

```markup
  <section xsi:type="DiagnosticsConfigurationSection">
    <sources>
      <add name="SanteDB.Core.DataSet" filter="Warning"/>
    </sources>
    <writers>
      <add name="console" initializationData="" filter="Informational">
        <writer>SanteDB.Core.Diagnostics.ConsoleTraceWriter, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null</writer>
      </add>
    </writers>
  </section>
```

### Source Filters

By default, all log requests are sent to the logging infrastructure, you can, however, control/filter the events from each source by adding it to the &lt;sources&gt; element. For example, to have the FHIR logs at level Error and the HL7v2 logs at Warning:

```markup
    <sources>
      <add name="SanteDB.Messaging.FHIR" filter="Error" />
      <add name="SanteDB.Messaging.HL7" filter="Warning" />
    </sources>
```

When configured in this manner, only errors reported by the FHIR source will be logged to the application logs.

### Log Writers

Writers are registered/configured in the &lt;writers&gt; element and are given a name, initialization data \(like file name, port number, etc.\) and a filter.

```markup
<writers>
      <add name="main" initializationData="santedb.log" filter="Warning">
        <writer>SanteDB.Core.Diagnostics.RolloverTextWriterTraceWriter, SanteDB.Core, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null</writer>
      </add>
```

The writers which are available in SanteDB iCDR and dCDR are:

| Writer | Logs To |
| :--- | :--- |
| SanteDB.Core.Diagnostics.ConsoleTraceWriter | Console |
| SanteDB.Core.Diagnostics.RolloverTraceWriter | Specified file |
| SanteDB.Core.Diagnostics.SystemDiagnosticsTraceWriter | .NET Trace Writer infrastructure |
| SanteDB.Core.Diagnostics.EventLogTraceWriter | Windows Event Log |
| SanteDB.DisconnectedClient.Android.Core.Diagnostics.AndroidLogTraceWriter | Android device developer log |



