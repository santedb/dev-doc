# Data Configuration

The DataConfigurationSection is used to control the internal connection strings used by the iCDR or the dCDR.

```markup
  <section xsi:type="DataConfigurationSection">
    <connectionStrings>
      <add name="PSQL" value="server=localhost;port=5432; database=santedb; user id=postgres; password=postgres; pooling=true; MinPoolSize=5; MaxPoolSize=10; Timeout=60; " provider="Npgsql"/>
      <add name="AUDIT" value="server=localhost;port=5432; database=santedb_audit; user id=postgres; password=postgres; pooling=true; MinPoolSize=5; MaxPoolSize=10; Timeout=60; " provider="Npgsql"/>
    </connectionStrings>
  </section>
```

{% hint style="info" %}
SanteDB defines its own ADO.NET configuration to ensure portability of plugins across various platforms.
{% endhint %}



