# HL7 Authentication

## Node Authentication using Message

If your deployment does no leverage client certificates for authentication, then your configuration must supply a configuration in the `security` attribute for the configuration. It can have one of the values drawn from the list below, which impact the method with which clients are authenticated.

### No Authentication

When the `None` authentication method is specified, then the SanteDB server will use the value of `MSH-3` as an application identity, and the configured `noAuthSecret` as the client secret.&#x20;

{% hint style="danger" %}
This configuration option is only recommended if it is impossible to use X509 certificates or MSH-8 or SFT-4 authentication schemes. All `MSH-3` values will share the same secret.
{% endhint %}

### MSH-8 Authentication

When the `Msh8` option is specified for security mode, then SanteDB server will use the following authentication strategy:

| MSH-8     | App ID  | App Secret     | Dev ID         | Dev Secret |
| --------- | ------- | -------------- | -------------- | ---------- |
| `FOO+BAR` | `MSH-3` | `BAR`          | `MSH-3\|MSH-4` | `FOO`      |
| `FOOBAR`  | `MSH-3` | `noAuthSecret` | `MSH-3\|MSH-4` | `FOOBAR`   |

### SFT-4 Authentication

When `Sft4` is used as the security mode, then SanteDB server will use the following authentication strategy:

| App ID  | App Secret | Dev ID         | Dev Secret |
| ------- | ---------- | -------------- | ---------- |
| `MSH-3` | `SFT-4`    | `MSH-3\|MSH-4` | `MSH-8`    |

{% hint style="info" %}
SFT-4 is only supported on newer version of HL7 and should not generally be used unless a reliable software binary value is provided.
{% endhint %}

## Node Authentication using x.509 Certificates

If your use case requires remote servers to enforce client authentication using X.509 certificates, the configuration is modified to add a client certificate or client certificate authority as:

```markup
 <add address="sllp://0.0.0.0:2200" receiveTimeout="0" name="SanteMPI IHE SLLP">
  <sllp checkCrl="true" requireClientCert="true">
    <serverCertificate findType="FindByThumbprint" storeLocation="LocalMachine" findValue="467808134ADFFA873694261C707016EC03080A86" />
    <clientAuthorityCertificate findType="FindByThumbprint" storeLocation="LocalMachine" findValue="F62FBFA197D0B71207D504D1C7B39598B72C47FD" />
  </sllp>
```

When using X.509 authentication the HL7 message handler will use the `MSH-3|MSH-4` value as the device name and the thumbprint of the selected X.509 certificate as the secret. Additionally, the X.509 certificate must have a chain which includes the certificate indicated in `<clientAuthorityCertificate`.

When node authentication is perform using certificates, the value of the `securityMode` attribute dictates the authentication strategy for the application (`MSH-3`). Where:

| Security Mode | Authentication                                                                           |
| ------------- | ---------------------------------------------------------------------------------------- |
| None          | No application authentication is performed - the system application is used              |
| Msh8          | The entire value of the `MSH-8` segment is used as the client secret for the application |
| Sft4          | The entire value of the `SFT-4` segment is used as the client secret for the application |

{% hint style="info" %}
You can use the SanteDB Configuration Tool's [hl7-version-2-service.md](../../../operations/server-administration/configuration-tool/messaging-settings/hl7-version-2-service.md "mention") to configure these options in the user interface.
{% endhint %}
