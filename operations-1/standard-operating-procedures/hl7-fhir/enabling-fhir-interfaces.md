# Enabling FHIR Interfaces

To enable the HL7 FHIR interface on your SanteDB iCDR you will need to:

* Enable the FHIR Message Service in your host context
* Configure the FhirServiceConfigurationSection
* Optionally enable FHIR audit dispatcher notifications

## Enabling the FHIR Interface

### Enable the FHIR Message Handler Services

To enable the FHIR message handler, you should include the following option in your `santedb.config.xml` file:

```markup
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="8">
    <serviceProviders>
      <add type="SanteDB.Messaging.FHIR.FhirMessageHandler, SanteDB.Messaging.FHIR, Version=2.1.0.0, Culture=neutral, PublicKeyToken=null" />
      <add type="SanteDB.Messaging.FHIR.FhirDataInitializationService, SanteDB.Messaging.FHIR, Version=2.1.0.0, Culture=neutral, PublicKeyToken=null" />
    </serviceProviders>
</section>
```

This enables two services for FHIR:

* `FhirMessageHandler`: Which is responsible for the processing of FHIR messages over HTTP REST
* `FhirDataInitializationService`: Which is responsible for the import of FHIR resource files from the hard disk drive in the `/data/fhir` directory.

Alternately, you can enable the FHIR services via the environment variable (in Docker or Kubernetes) using:

```
SDB_FEATURE=...;FHIR;...
```

### Configuring FHIR Message Handler

The FHIR Message Handler uses the `FhirServiceConfigurationSection` in order to drive the configuration of the FHIR services.&#x20;

```markup
<SanteDBConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="2.1.0.0" xmlns="http://santedb.org/configuration">
  <sections>
    <add type="SanteDB.Messaging.FHIR.Configuration.FhirServiceConfigurationSection, SanteDB.Messaging.FHIR, Version=2.1.0.0, Culture=neutral, PublicKeyToken=null" />
  </sections>
  <!-- Truncated for space -->
  <section xsi:type="RestConfigurationSection">
    <!-- -->
    <service name="FHIR">
      <behaviors>
        <add type="SanteDB.Rest.Common.Security.TokenAuthorizationAccessBehavior, SanteDB.Rest.Common" />
      </behaviors>
      <endpoint contract="SanteDB.Messaging.FHIR.Rest.IFhirServiceContract, SanteDB.Messaging.FHIR" address="http://0.0.0.0:8080/fhir">
        <behaviors>
          <add type="SanteDB.Rest.Common.Behavior.MessageLoggingEndpointBehavior, SanteDB.Rest.Common" />
          <add type="SanteDB.Rest.Common.Behavior.MessageCompressionEndpointBehavior, SanteDB.Rest.Common" />
          <add type="SanteDB.Rest.Common.Behavior.MessageDispatchFormatterBehavior, SanteDB.Rest.Common" />
          <add type="SanteDB.Rest.Common.Behavior.AcceptLanguageEndpointBehavior, SanteDB.Rest.Common" />
        </behaviors>
      </endpoint>
    </service>
    
  </section>
  
  <section xsi:type="FhirServiceConfigurationSection">
    <resourceHandlers>
      <!-- Resources enabled on this server as type references for example:
      <add type="SanteDB.Messaging.FHIR.Handlers.AdverseEventResourceHandler, SanteDB.Messaging.FHIR" />
      -->
    </resourceHandlers>
    <resources>
      <!-- Resources enabled on this server as resource type names, for example:
      <add type="Patient"/>
      -->
    </resources>
    <operationHandlers>
      <!-- Custom fhir operation handlers enabled on this instance, for example:
      <add type="SanteMPI.Messaging.IHE.FHIR.PatientIdentityCrossReferenceMobileOperation, SanteMPI.Messaging.IHE" />
      -->
    </operationHandlers>
    <operations>
       <!-- Custom operations which are enabled on this instance, for example:
       <add>ihe-pix</add>
       <add>process-message</add>
       -->
    </operations>
    <messageHandlers>
      <!-- Custom message operations / message handlers , for example:
      <add type="SanteMPI.Messaging.IHE.FHIR.PatientMasterIdentityOperation, SanteMPI.Messaging.IHE" />
      -->
    </messageHandlers>
    <messages>
       <!-- Custom message operations by the URN of the message event, for example:
       <add>urn:fhir:message:foo</add>
       -->
    <extensionHandlers>
       <!-- Custom extension handlers for process/producing extensions, for example:
      <add type="SanteMPI.Messaging.IHE.FHIR.MothersMaidenNameExtension, SanteMPI.Messaging.IHE" />
     -->
    </extensionHandlers>
    <extensions>
       <!-- Custom extensions to enable on this instance -->
    </extensions>
    <base><!-- Base URL for producing absolute references --></base>
    <behaviorModifiers>
      <!-- Custom behaviors which should be enabled on this FHIR service :
      <add type="SanteMPI.Messaging.IHE.FHIR.PatientIdentityCrossReferenceMobileOperation, SanteMPI.Messaging.IHE" />
      -->
    </behaviorModifiers>
  </section>
 
</SanteDBConfiguration>
```

#### REST Configuration

The endpoint on which the service listens is driven by the `RestConfigurationSection` , a service with name `FHIR` is registered with one or more `<endpoint>` elements which dictate the IP/Port and scheme of binding.

{% hint style="info" %}
As with all SanteDB services, it is recommended to use SSL termination at an upstream host. The HTTPS scheme is only supported on Windows and only after an appropriate `netsh http sslcert add` command has been executed to bind a certificate to the WinHTTP layer.
{% endhint %}

#### Controlling Resource Access

By default, the FHIR message handler will scan the application domain for all resource handlers and will, by default, enable all available resources. There are use cases where this list of resources needs to be constrained for a particular SanteDB role (for example, in SanteMPI it may not be advisable to expose the AdverseEvent resource handlers).

To enable a resource on the FHIR handler using the default implementation of the resource handler, appropriate `<resources>` should be registered in the configuration section, for example, to enable only Patient and RelatedPerson:

```
<resources>
   <add type="Patient"/>
   <add type="RelatedPerson"/>
</resources>
```

Alternately, if you would like to implement a custom resource handler which can provides specific behaviours for a particular resource type, you can use the `<resourceHandlers>` section and provide an assembly-qualified pointer to the resource handler:

```
<resourceHandlers>
    <add type="Sample.Custom.FHIR.Handlers.PatientHandler, Sample.Custom"/>
```

#### Extended Operations and Extensions

The [Extending FHIR Functionality](extending-fhir-interfaces.md) wiki article described the process of extending the FHIR interface with custom operations and custom extensions.

## Configuring Dispatcher Targets

FHIR dispatchers are classes which are responsible for sending data from your SanteDB iCDR server to another server. These dispatchers can be created using a `Subscription` resource, or can be the FHIR Audit Dispatcher (described below).&#x20;

The configuration for these dispatchers are driven by the settings in the `Subscription` resource, however can further be configured using `FhirDispatchConfigurationSection`.

```markup
  <sections>
    <add type="SanteDB.Messaging.FHIR.Configuration.FhirDispatcherConfigurationSection, SanteDB.Messaging.FHIR, Version=2.1.0.0, Culture=neutral, PublicKeyToken=null" />
  </sections>

  <section xsi:type="FhirDispatcherConfigurationSection">
    <targets>
      <add>
        <name>audit</name>
        <endpoint>http://localhost:8989/fhir/Audit</endpoint>
        <user>user_to_authenticate</user>
        <password>password_to_authenticate</password>
        <authenticator type="Class.Of.Authenticator" />
      </add>
    </targets>
  </section>
```

By default, the `<user>` and `<password>` fields are used to drive HTTP BASIC authentication, however a custom `<authenticator` can be used if the target service requires obtaining a security certificate, an authorization token, etc.&#x20;

{% hint style="info" %}
To modify/customize a `Subscription` resource , a `<target>` is added with `<name>` matching the id of the subscription.
{% endhint %}

## Enabling FHIR Audits

All message layer functions in SanteDB produce audits which are stored in the local SanteDB audit repository instance (or in the [SanteGuard audit repository](../../../santeguard/introduction.md) if installed). These audits can optionally be shipped or forwarded to another audit repository by enabling an `IAuditDispatcher` service.

The FHIR service in SanteDB contains a FHIR based audit dispatcher which creates instances of `AuditEvent` and ships them to a FHIR server. To enable the FHIR audit dispatcher, add it as a service in your service configuration:

```markup
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="8">
    <serviceProviders>
      <add type="SanteDB.Messaging.FHIR.Auditing.FhirAuditDispatcher, SanteDB.Messaging.FHIR, Version=2.1.0.0, Culture=neutral, PublicKeyToken=null" />
    </serviceProviders>
```

In Docker or Kubernetes, this feature is enabled using:

```
SDB_FEATURE=...;FHIR_AUDIT;...
```

After configuration of the audit dispatcher, you will need to configure a dispatcher target named `AUDIT` which provides the destination registration of where to send the audit information. In Kubernetes/Docker this is configured with:

```
SDB_FHIR_AUDIT_EP=http://target:port/path
SDB_FHIR_AUDIT_UN=user_to_authenticate
SDB_FHIR_AUDIT_PWD=password_to_authenticate
SDB_FHIR_AUDIT_AUTH=AuthenticatorType
```
