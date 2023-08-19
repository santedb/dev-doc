# Securing SanteDB Configuration

The `santedb.config.xml` file contains sensitive information such as database connection strings, certificate and digital signing keys, shared secrets, etc. This information can be protected in SanteDB via encryption.

When encrypting your configuration file, certain sections will become protected, and their contents will appear in the configuration file as:

```xml
  <section xsi:type="SanteDBProtectedConfigurationSectionWrapper" 
      t="SanteDB.Core.Security.Configuration.SecurityConfigurationSection, SanteDB.Core.Api, Version=3.0.995.0, Culture=neutral, PublicKeyToken=null">
    <c>aC54/S88bLf6sHTKFf3kIdeckI5PbsovdQiwty9CdncAeP823PS3PBbARZ7fSoOdNJUtPAEg+....</c>
    <i>EmzcwxBg0FhIM8SoH76cKQ==</i>
  </section>
```

## Protecting your Configuration File

If you are using the [Configuration Tool](../../../operations/server-administration/configuration-tool/#protected-configurations), will be prompted on configuration save on Windows to select a configuration protection certificate. On Linux, or Docker the configuraiton is performed manually. To do this, copy the thumbprint of the certificate with which you'll be protecting your configuration and run:

```
sanatedb --reencrypt --config=santedb.config.xml
```

You will be prompted for the thumbprint of your certificate, and your configuration file will be encrypted.

{% hint style="danger" %}
You should not share encrypted configuration files between servers. If your configuration file is on a shared drive between application servers, you must ensure that the private key for the certificate is available on each of the servers.
{% endhint %}

{% hint style="info" %}
You may be prompted whether you want to apply the certificate to your ALE environment.
{% endhint %}
