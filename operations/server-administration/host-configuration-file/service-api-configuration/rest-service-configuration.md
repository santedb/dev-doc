# REST Service Configuration

The RestService configuration is contained in the `RestConfigurationSection` section. To register this section, add the following section configuration registration.

```markup
<sections>
  <add type="SanteDB.Server.Core.Configuration.RestConfigurationSection, SanteDB.Server.Core" />
</sections>
```

Each REST based service in the host uses a service in the rest controller host (listed as service sections). The basic architecture of the REST service layer is illustrated below.

![](<../../../../../.gitbook/assets/image (200).png>)

* **Service:** A service represents a logical service which is provided on the REST based API. A service can be FHIR or METADATA, etc. Typically a single daemon service will bind itself to a single rest service.
* **Service Behavior:** Service behaviors represent a behavior which applied across all endpoints within the service. This can be, for example, authorization behaviors, or policy behaviors.
* **Endpoint:** An endpoint is a specific listening location for the REST based service. The endpoint is bound to a listening address and a contract. A contract can express a particular series of operations and paths on the endpoint base address.  A contract can be (for example) v1, v2, v3 of an API service.
* **Endpoint Behavior:** An endpoint behavior is a particular behavior applied only to the endpoint. Endpoint behaviors include messaging inspectors, serializers, compression behaviors, cors behaviors etc.

An example of a simple FHIR API configuration is illustrated below.

```markup
<service name="FHIR">
      <behaviors>
        <add type="SanteDB.Server.Core.Rest.Security.TokenAuthorizationAccessBehavior, SanteDB.Server.Core, Version=2.1.0.0"/>
      </behaviors>
      <endpoint address="http://0.0.0.0:8080/fhir" contract="SanteDB.Messaging.FHIR.Rest.IFhirServiceContract, SanteDB.Messaging.FHIR, Version=2.1.0.0">
        <behaviors>
          <add type="SanteDB.Rest.Common.Behavior.MessageLoggingEndpointBehavior, SanteDB.Rest.Common, Version=2.1.0.0"/>
        </behaviors>
      </endpoint>
    </service>
```

## Services

The following services are bound to the REST API in the default SanteDB installation.

| Service Name | Plugin                                                                                                                                                               |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OAuth2       | [SanteDB OpenID Connect IdP](../../../../../developers/extending-santesuite/extending-santedb/service-apis/openid-connect/)                                          |
| FHIR         | [HL7 FHIR Interface](../../../../../operations-1/standard-operating-procedures/hl7-fhir/)                                                                            |
| AMI          | [Administrative Management Interface](../../../../../developers/extending-santesuite/extending-santedb/service-apis/administration-management-interface-ami/)        |
| BIS          | [Business Intelligence Service](../../../../../developers/extending-santesuite/extending-santedb/server-plugins/service-definitions/business-intelligence-services/) |
| HDSI         | [Health Data Service Interface](../../../../../developers/service-apis/health-data-service-interface-hdsi.md)                                                        |
| META         | OpenAPI (Swagger) Metadata Exchange                                                                                                                                  |

## Service Behaviors

### Token Authorization Access

The TokenAuthorizationAccess behavior is configured using the `SanteDB.Server.Core.Rest.Security.TokenAuthorizationAccessBehavior.` This service validates bearer tokens with the current ISessionManager service and allows the establishment of a principal.&#x20;

```markup
<service name="name">
  <behaviors>
    <add type="SanteDB.Rest.Common.Security.TokenAuthorizationAccessBehavior, SanteDB.Rest.Common"/>
  </behaviors>
```

### Basic Authentication Access Behavior

The BasicAuthenticationAccessBehavior behavior is configured using the `SanteDB.Rest.Common.Security.BasicAuthorizationAccessBehavior` and allows the use of HTTP BASIC authentication to establish principals.

```markup
<service name="name">
  <behaviors>
    <add type="SanteDB.Rest.Common.Security.BasicAuthorizationAccessBehavior, SanteDB.Rest.Common"/>
  </behaviors>
```

### Client Authorization Access Behavior

The ClientAuthorizationAccessBehavior allows services to authenticate client credentials using basic authorization. This establishes an `ApplicationPrincipal` as the primary principal.

```markup
<service name="name">
  <behaviors>
    <add type="SanteDB.Authentication.OAuth2.Wcf.ClientAuthorizationAccessBehavior, SanteDB.Authentication.OAuth"/>
  </behaviors>
```

## Endpoint Behaviors

The endpoint behaviors listed here control the behavior of individual endpoints on the SanteDB core service.

### Message Logging Behavior

The message logging endpoint behavior will log all inbound messages to the primary trace source log.

```markup
<endpoint address="address" contract="contract">
        <behaviors>
          <add type="SanteDB.Rest.Common.Behavior.MessageLoggingEndpointBehavior, SanteDB.Rest.Common"/>
        </behaviors>
</endpoint>      
```

### Message Compression Behavior

The message compression endpoint behavior enables the message compression ability on the server and allows clients to send `Accept-Encoding:` headers with algorithm gzip, bzip2, deflate or lzma.

```markup
<endpoint address="address" contract="contract">
        <behaviors>
          <add type="SanteDB.Rest.Common.Behavior.MessageCompressionBehavior, SanteDB.Rest.Common"/>
        </behaviors>
</endpoint>    
```

### CORS Behavior

The CORS endpoint behavior allows cross origin requests to be executed on a specific endpoint. The CORS behavior accepts a configuration which dictates the CORS policies for the service.

```markup
<endpoint address="address" contract="contract">
        <behaviors>
          <add type="SanteDB.Rest.Common.Behavior.CorsEndpointBehavior, SanteDB.Rest.Common, Version=2.1.0.0">
            <configuration>
              <CorsEndpointBehaviorConfiguration>
                <resource name="*" domain="*">
                  <verbs>
                    <add>OPTIONS</add>
                    <add>POST</add>
                    <add>PUT</add>
                    <add>PATCH</add>
                    <add>DELETE</add>
                    <add>GET</add>
                  </verbs>
                  <headers>
                    <add>Content-Type</add>
                    <add>Accept-Encoding</add>
                    <add>Content-Encoding</add>
                  </headers>
                </resource>
              </CorsEndpointBehaviorConfiguration>
            </configuration>
          </add>
        </behaviors>
</endpoint>   
```

### Accept Language Behavior

The accept language behavior allows the SanteDB instance to modify the current localization string for errors and responses on the CDR pipeline. This handler uses the following language preferences in the following order:

1. The language of the user's session
2. The value of the Accept-Language header
3. The value of the X-Sdb-Language header (used when clients cannot set Accept-Language)

### Security Policy Behavior

The security policy behavior enables cross site scripting and [Content Security Policy (CSP) ](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)on the endpoint.

```markup
<endpoint address="address" contract="contract">
        <behaviors>
          <add type="SanteDB.Rest.Common.Behavior.SecurityPolicyHeadersBehavior, SanteDB.Rest.Common"/>
        </behaviors>
</endpoint>    
```

