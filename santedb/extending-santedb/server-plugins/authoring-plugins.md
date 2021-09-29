---
description: >-
  This section describes the necessary steps and procedures to author your own
  C#/.NET based plugins
---

# Authoring Plugins

When authoring a plugin, it is important to understand the function of the plugin and how it will/should be used in the SanteDB host process.

## Plugin Libraries

All SanteDB components \(the iCDR, dCDR, and UI\) all leverage common packages. These packages are shared among a variety of the infrastructure components. 

![Library Relationship](../../../.gitbook/assets/image%20%2886%29.png)

When implementing your plugin, if, for example, you target .NET Framework and use the SanteDB.Server.Plugin package, then your plugin will not work on the dCDR. Conversely if you only reference APIs in the SanteDB Core Libs package then your plugin will work on all platforms SanteDB supports.

The general rule is:

* If you're creating a global .NET plugin select .NET Standard 2.0 as the project type
* If you're creating a SanteDB dCDR based plugin use either .NET Standard 2.0 or .NET Framework 4.7 
* If you're creating a SanteDB iCDR based plugin use .NET Framework 4.7

## Adding Nuget Dependencies

Once you've decided where your plugin fits into the SanteDB ecosystem you'll have to add your Nuget dependencies. All SanteDB Nuget packages are registered on the central Nuget repository, the table below identifies which SanteDB Nuget packages provide which functionality.

## Digital Signature Requirements

Starting with SanteDB iCDR and dCDR version 2.1.80 \(Paris\) both the dCDR and iCDR require that all .NET assemblies which are registered for service use are digitally signed. There are two ways you can sign your .NET plugins for use in a release version of SanteDB.

The requirement of digital signatures on .NET code ensures that:

* The plugin comes from a reputable company which has been validated by a third party source or by the SanteSuite community.
* The plugin code has not been tampered with since the publisher compiled and signed the assembly.
* Verifies the publisher of the plugin \(opposed to a self-assertion by the publisher\)

When set to `Informational` log level you will see log entries indicating successful validation of the plugin:

```text
SanteDB.Core.Services.Impl.DependencyServiceManager@ <Informational> [2021-09-28T18:19:26.0273659-04:00]: Validating SanteDB.Server.dll published by CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
SanteDB.Core.Services.Impl.DependencyServiceManager@ <Informational> [2021-09-28T18:19:26.0273659-04:00]: SanteDB.Server.dll was validated as trusted code
```

When code is not digitally signed , any services provided by that assembly will not be loaded and an error log message will appear:

```text
santedb Error: 0 : Fatal exception occurred: System.Security.SecurityException: Service MyPlugin.MyService in assembly MyPlugin.dll is not signed - or its signature could not be validated! Plugin may be tampered!
```

### Validating Digital Signatures

On Microsoft Windows operating systems you can validate digital signatures and publishers of a plugin by right clicking on the plugin in Windows Explorer and using the `Digital Signatures` tab of the properties window.  


![Viewing Digital Signatures](../../../.gitbook/assets/image%20%28404%29.png)

By clicking `Details` you can view the digital signature on the assembly code and validate the issuer and publisher of the digital signature. 

![Certificate Details](../../../.gitbook/assets/image%20%28406%29.png)

### Disabling Code Validation

You can disable code validation by setting the `allowUnsignedAssemblies` attribute on the `ApplicationServiceContextConfigurationSection` as:

```markup
<section xsi:type="ApplicationServiceContextConfigurationSection"
    threadPoolSize="8"
    allowUnsignedAssemblies="true">
```

{% hint style="danger" %}
You should only use this setting for development and debugging environments \(such as when referencing the `SanteDB` Nuget package\). If disabled, the host service will load and execute any assembly code contained in the configuration file.
{% endhint %}

### Obtaining a Code Signing Certificate

#### Registered Authenticode Provider

If you're compiling a general purpose plugin or SanteDB distribution, or are writing other software which will need to be installed on Microsoft Windows, Linux, etc. it is recommended you use a registered [Microsoft Authenticode SSL Provider](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/authenticode) . These certificates typically cost between $200 and $800 per year , however they are recognized by Microsoft Windows and other operating systems and are generally more portable than other options.

#### SanteSuite Software Publisher Certificates

If you're only developing software for SanteDB and wish only to publish extensions and plugins for SanteDB, you may obtain a publishing certificate from the SanteSuite community. These community certificates are only trusted by SanteDB iCDR and dCDR software packages, which means they are less suited for general purpose software development.

In order to obtain a certificate from SanteSuite community you will need to become a [SanteDB Software Publisher](../../santedb/santedb-software-publishers.md). 

#### Self-Signed Publisher Certificate

Finally, you can create your own self-signed code signing certificate. This is less ideal as it restricts the portability of your software extension. In order to use self-signed code certificates you will need to:

1. Generate a private key with extended use of `codeSigning` \(optionally sign it with your own CA's certificate\).
2. Export the private key, certificate, and CA's certificate \(forming an X509 chain\) to a PKCS12 \(`.pfx`\) file.
3. Import the CA's certificate into the trust store
   1. On Windows this is done by placing the certificate in the `Trusted Publishers` store on all machines which will use the plugin
   2. On Mono \(Linux, Docker, MacOS\) you should use [Mono's certificate tools ](https://www.mono-project.com/docs/faq/security/)to manage the certificates.

