# Securing SanteDB APIs

If you are running SanteDB iCDR or dCDR in a context where they need to be accessed from outside the datacenter, you will need to setup the services to use TLS.&#x20;

This will require obtaining an SSL certificate, installing the certificate into the local certificate store using either:

* Microsoft Management Console (`mmc`) Certificates snap-in.
* `certmgr` on Mono (Linux or Mac)
* SSL Termination (for REST APIs only)

Securing the HL7v2 interfaces is documented in [SanteDB HL7v2 Implementation](../../../developers/service-apis/administration-management-interface-ami/santedb-hl7v2-implementation.md#tls-+-llp-sllp) and is not covered here.

## Securing iCDR and dCDR Directly

### Microsoft Windows Operating Systems

If installing SanteDB on Microsoft Windows, you should obtain a security certificate from a certificate authority. Once obtained, install the certificate into the Machine context of the host operating system.

1.  Press (WIN)+R and type `mmc`&#x20;

    <img src="../../../.gitbook/assets/image (431) (1) (1) (1) (1) (1).png" alt="" data-size="original">
2.  Use File -> Add/Remove Snap-In and select Certificates

    ![](<../../../.gitbook/assets/image (426) (1) (1) (1) (1) (1) (1).png>)
3.  Select the Computer Account and ensure the local server is the target

    ![](<../../../.gitbook/assets/image (425) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
4.  Import your certificate and private key (which you generated to get the certificate) into the Personal store. When completed you should see the certificate with a key indicator

    ![](<../../../.gitbook/assets/image (421) (1) (1) (1) (1) (1) (1) (1).png>)



Once this is complete, you should use the [SanteDB Configuration Tool Certificate Binding](../../../operations/server-administration/configuration-tool/messaging-settings/#certificate-binding) to bind the certificate to the service and endpoint.

#### Securing dCDR Installations

You can also secure dCDR instances, however the process is a manual one. First, you should configure the dCDR web or gateway service like you normally would (i.e. join the domain and ensure you can login with `localhost:9200`)

1.  Obtain the certificate thumbprint information from the certificate details:

    ![](<../../../.gitbook/assets/image (422) (1) (1) (1) (1) (1) (1).png>)
2. In an elevated command prompt, bind the dCDR HTTP listener port to the certificate via `netsh` for example: `netsh http add sslcert ipport=0.0.0.0:9200 appid={A97FB5DE-7627-401C-8E70-5B96C1A0073B} certhash=<hash-of-your-cert>`
3. If your dCDR instance is running as a less privileged account (other than `LOCAL SERVICE`) then you will need to reserve the URL: `netsh http add urlacl url=http://+:9200 user=<user-of-service>`
4. In an elevated text editor (like notepad) open `%systemroot%\SysWOW64\config\systemprofile\AppData\Roaming\santedb-www\default\SanteDB.config`
5. You should edit the `RestConfigurationSection` and bind each of the service ports from `http://127.0.0.1:9200` to `https://127.0.0.1:9200`&#x20;
6. Save the configuration file
7. Restart the SanteDBWWW service

## Using NGINX Reverse Proxy

The best way to run SanteDB iCDR and dCDR services is behind a reverse proxy using NGINX. This allows the components within the data center to communicate directly with one another (on a secure private network) without TLS overhead and only uses encryption when data leaves the private network.

To use NGINX you will have to create a `/etc/nginx/services-available/name.domain.com` file with the following contents. The configuration has two pieces:

1. A configuration for the secured service you're exposing (recommended 8443 for iCDR and 443 for dCDR)
2. A configuration for the unsecured service which redirects to the secured port.

```
# Example of iCDR API
server {
        listen 8443 ssl;
        listen [::]:8443 ssl;

        # For dCDR you should maybe use
        # listen 443 ssl;
        # listen [::]:443 ssl;
        
        # These should be the X509 cert and private key
        # you got from your CA
        ssl_certificate /etc/nginx/ssl/my_cert.crt;
        ssl_certificate_key /etc/nginx/ssl/my_key.rsa;

        # This is the host name of the server you're binding to
        server_name name-of-your-server.net;

        location / {
                # Forward to app server
                proxy_pass http://internal-ip-address:8080/;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_cookie_domain internal-ip-address name-of-your-server.net;
                proxy_pass_request_headers on;
        }
}

# Server redirects any unsecured requests to secured
server {
        listen 8080;
        listen [::]:8080;
        server_name name-of-your-server.net;
        return 301 https://$host$request_uri;
}
```

You should then link this file to the `/etc/nginx/sites-enabled` directory and restart nginx.

## Client Certificates

You can secure the SanteDB APIs using dual-PKI (public key infrastructure) authentication. This method of API security will require that a remote node present a valid, trusted RSA certificate prior to any application level logic being executed. There are some configurations where this strategy can be deployed:

1. Securing the OAUTH endpoint so that devices must present a certificate prior to obtaining an access token.
2. Securing all API endpoints so that even those with valid access tokens must present the certificate.

{% hint style="info" %}
In order to use client certificate authentication, the SanteDB iCDR or dCDR must be configured to use HTTPS as described in the above instructions. If using NGINX as a TLS termination point, the PEM for the certificate must be passed to the SanteDB server in the `X-SSL-ClientCert` header.
{% endhint %}

Configuring the client certificates first requires the `netsh` command to be used to require client certificates:

```
netsh http add sslcert ipport=0.0.0.0:8443 certhash={your-certificate-for-the-server} 
   appid={A97FB5DE-7627-401C-8E70-5B96C1A0073B} clientcertnegotiation=true
```

Next an implementation of the `ICertificateIdentityProvider` must be configured in the SanteDB service. This service maps an X509 certificate to a user, device, or application. In your `<services>` node, add a reference to the certificate handler.&#x20;

```
<add type="SanteDB.Persistence.Data.Services.AdoCertificateIdentityProvider, SanteDB.Persistence.Data" />
```

Next, the endpoints in the SanteDB configuration file need to be changed from `http://` scheme to `https://` scheme, and the `ClientCertificateAccessBehavior` added to the service. For example, if your OAUTH configuration is:

```xml
<service name="OAuth2" 
  implementationType="SanteDB.Rest.OAuth.Rest.OAuthServiceBehavior, SanteDB.Rest.OAuth">
  <behaviors>
  </behaviors>
  <endpoint contract="SanteDB.Rest.OAuth.Rest.IOAuthServiceContract, SanteDB.Rest.OAuth" 
     address="http://0.0.0.0:8443/auth">
    <behaviors />
  </endpoint>
</service>
```

Then the configuration to use client certificates should be updated to:

```xml
<service name="OAuth2" 
    implementationType="SanteDB.Rest.OAuth.Rest.OAuthServiceBehavior, SanteDB.Rest.OAuth">
  <behaviors>
    <add type="SanteDB.Rest.Common.Security.ClientCertificateAccessBehavior, SanteDB.Rest.Common">
      <configuration>
          <ClientCertificateAccessConfiguration revokeCheck="Online">
            <allowClientHeader>false</allowClientHeader>
            <trustedIssuers>
              <add findType="FindByThumbprint" storeName="My" storeLocation="LocalMachine" findValue="59EC967D51DA999AB4EE0E082C12ED288DD05FAB" />
            </trustedIssuers>
          </ClientCertificateAccessConfiguration>
        </configuration>
    </add>
  </behaviors>
  <endpoint contract="SanteDB.Rest.OAuth.Rest.IOAuthServiceContract, SanteDB.Rest.OAuth" 
    address="https://0.0.0.0:8443/auth">
    <behaviors />
    <certificate findType="FindByThumbprint" storeName="My" storeLocation="LocalMachine" findValue="59EC967D51DA999AB4EE0E082C12ED288DD05FAB" />
    <clientCerts>true</clientCerts>
  </endpoint>
</service>
```

The `<configuration>` element of the client certificate access behavior controls how the access behavior validates the client certificate including.

| Option            | Values                | Description                                                                                                                                                                                                |
| ----------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| revokeCheck       | Online, Offline, None | Controls how client certificates' revokation status is validated.                                                                                                                                          |
| allowClientHeader | true, false           | Indicates whether the `X-SSL-ClientCert` header is to be allowed. Note: **If running behind NGINX with SSL termination this must be true, if not it is recommended to be false.**                          |
| trustedIssuers    | X509 Certificate      | The trusted issuers of client certificates. If the client presents a certificate that is valid to the operating system, however is not issued by a CA in this list then the access request will be denied. |

### Client Certificates Behind a Reverse Proxy

When using client certificate authentication and a reverse proxy - the TLS session is dropped (and optionally re-established afterwards). This prevents the SanteDB iCDR from determining the identity of the secure node accessing the API beyond the proxy.&#x20;

If your reverse proxy natively supports forwarding the TLS session (and client certificate) this is the preferred method. However, if using client certificate authentication behind a reverse proxy which cannot re-authenticate via client certificate the reverse proxy can emit the `X-SSL-ClientCert` header on the request to the iCDR behind the proxy.&#x20;

For example, in NGINX the configuration for `proxy_pass` would be:

```
   ## Configuration Truncated
   ## Have NGINX validate the certificate
   ssl_client_certificate /etc/ssl/certs/ca.crt;
   ssl_verify_client on;
   location / {
     # Forward to app server
     proxy_pass http://internal-ip-address:8080/;
     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
     proxy_cookie_domain internal-ip-address name-of-your-server.net;
     proxy_pass_request_headers on;
     ## Attach a copy of the client certificate to the request for the iCDR to inspect
     proxy_set_header X-SSL-ClientCert $ssl_client_cert;
}
```

## Securing Default Applications

By default SanteDB's database contains credentials for applications which ship with SanteDB (such as the debugger, the admin console, the DCG, etc.). After deployment, it is recommended that system administrators perform the following actions:

1. Disable or lock any applications not being used (for example: if you are not using the DCG then disabling the gateway credential is recommended)
2. If an application is being used, reset the application secret (i.e. generate a new - non-default password for the application) this can be done via the SDBAC command `application.secret org.santedb.disconnected_client.gateway`)
3. Any application that does not require client authorization grants (i.e. non-interactive sessions) should have the `OAUTH client_credentials flow permission no device credential` set to DENY (you may use the SDBAC command: `application.grant <NAME OF APPLICATION> -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY` )

To perform this operation on all default applications in the SanteDB deployment the following script can be used:

```
## Reset client credentials
application.secret org.santedb.debug
application.secret org.santedb.disconnected_client.www
application.secret org.santedb.disconnected_client.win32
application.secret org.santedb.disconnected_client
application.secret org.santedb.ims
application.secret org.santedb.administration
application.secret org.santedb.disconnected_client.gateway
application.secret org.santedb.disconnected_client.android

## Lock Fiddler (debugging credential)
application.lock -l fiddler

## Remove the OAUTH Client Credentials Grant
application.grant org.santedb.debug -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.disconnected_client.www -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.disconnected_client.win32 -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.disconnected_client -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.ims -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.administration -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.disconnected_client.gateway -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
application.grant org.santedb.disconnected_client.android -p '1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0' -g DENY
```

{% hint style="info" %}
The `OAUTH client_credentials flow permission no device credential` policy permits applications to log into the OAUTH service with only a secret and an application ID. Denying this prevents this operation, however an application can continue to use the `client_credentials` when the `Authorization: BASIC <DEVICE CREDENTIAL>` is sent to the authorization endpoint.
{% endhint %}
