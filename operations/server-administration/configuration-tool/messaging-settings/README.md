# Messaging Settings

The messaging settings section allows system administrators to configure the various messaging interfaces on SanteDB.&#x20;

## Common REST Settings

The REST based services in the configuration panel have two sections of configuration in their panel, as illustrated in the FHIR panel below.

![](<../../../../.gitbook/assets/image (475).png>)

* REST API -> This section of the configuration panel is common to all REST services and controls the ports, paths and bindings of the REST API.
* Service -> This section varies and is specific to the actual API being configured.

This section illustrates the common REST settings.

<table><thead><tr><th width="216.2676612932232">Setting</th><th width="269.5026452105254">Description</th><th>Example</th></tr></thead><tbody><tr><td>Info Name</td><td>The informational name for the REST API. This is usually how the service handler knows which REST endpoint to bind to.</td><td><code>FHIR</code></td></tr><tr><td>Service Behaviors</td><td>The service behaviors configuration allows the configuration of one or more global behaviors for the service. Service behaviors are applied on all endpoints in the REST manager. See<a href="../../host-configuration-file/service-api-configuration/rest-service-configuration.md"> Service Behaviors</a></td><td>See: <a href="./#service-behaviors">Service Behaviors</a></td></tr><tr><td>Endpoints</td><td>The endpoints (port, scheme, and host) where the API should be accessed. See <a href="../../host-configuration-file/service-api-configuration/rest-service-configuration.md">Service Endpoints</a>.</td><td>See: <a href="./#endpoints">Endpoints</a></td></tr></tbody></table>

### Service Behaviors

The service behaviors option can be expanded to show a collection editor. Here, administrators can remove or add new behaviors to the service definition.



![](<../../../../.gitbook/assets/image (507).png>)

<table><thead><tr><th width="216.2676612932232">Setting</th><th width="269.5026452105254">Description</th><th>Examples</th></tr></thead><tbody><tr><td>Behavior Configuration</td><td>An XML fragment which controls the settings for the specific behavior. These change based on the behavior applied. See <a href="../../host-configuration-file/service-api-configuration/rest-service-configuration.md#service-behaviors">Service Behaviors </a>for more information.</td><td><code>&#x3C;maxConcurrency>10&#x3C;/maxConcurrency></code></td></tr><tr><td>Type</td><td>The type of behavior that should be applied to the service scope. This is the actual behavior implementation that will run.</td><td></td></tr></tbody></table>

### Endpoints

Editing the endpoints will present a collection editor where administrators can add/remove specific endpoint bindings to/from the service. Endpoint bindings dictate the port, scheme and path where the REST API can be accessed.

![](<../../../../.gitbook/assets/image (483).png>)



<table><thead><tr><th width="216.2676612932232">Setting</th><th width="269.5026452105254">Description</th><th>Example</th></tr></thead><tbody><tr><td>Address</td><td>The address where the service should listen. Binding to 0.0.0.0 instructs the API to listen on all bound IP addresses of the service, 127.0.0.1 will bind only to localhost. You can also specify a specific IP address assigned to the machine to bind to.</td><td><code>http://0.0.0.0:9000/fhir</code></td></tr><tr><td>Certificate Binding</td><td>The details of the security certificate to use for HTTPS traffic. See details on certificate configuration below.</td><td>See: <a href="./#certificate-binding">Certificate Binding</a></td></tr><tr><td>Endpoint Behaviors</td><td>Like the Service Behaviors configuration collection, this editor allows administrators to bind specific behaviors only to the specified endpoint. </td><td>See: <a href="./#service-behaviors">Service Behaviors</a></td></tr></tbody></table>

### Certificate Binding

When you set an endpoint address to scheme `https://` the certificate binding configuration is enabled.

![](<../../../../.gitbook/assets/image (502).png>)

When binding an endpoint to HTTPS you must ensure:

* The port is different than those used by HTTP bindings (only one scheme can be bound per port on a machine)
* You have an SSL certificate with a private key installed in one of the key stores available to Windows or Mono (on Mono - using `certmgr`)

Once the certificate binding is enabled, you can expand it and select the certificate

![](<../../../../.gitbook/assets/image (474).png>)



<table><thead><tr><th width="216.2676612932232">Setting</th><th width="269.5026452105254">Description</th><th>Examples</th></tr></thead><tbody><tr><td>Certificate</td><td>The selected certificate to use when serving requests on the API endpoint.</td><td><code>CN=localhost</code></td></tr><tr><td>Find Type</td><td>The method which should be used for finding the certificate in the secure store. If you're sharing this configuration across machines this value should be set appropriately to ensure that the correct certificate is selected..</td><td><p><code>FindByThumbprint</code> - The thumbprint of the X509 certificate is used to locate the certificate (<strong>recommended</strong>)</p><p><code>FindBySubjectName</code> - The subject name is used to find the certificate (recommended if a strong SN is present)</p></td></tr><tr><td>Location</td><td>The location where the SanteDB iCDR host should look for certificates.</td><td><p><code>LocalMachine</code> - Use the local machine context (<strong>recommended</strong>)</p><p><code>CurrentUser</code> - Use the service user account store.</p></td></tr><tr><td>Store</td><td>The store where SanteDB iCDR should look for the certificate to use for hosting the environment.</td><td><code>My</code> - The personal store of the service account/machine (<strong>recommended</strong>)</td></tr></tbody></table>

{% hint style="warning" %}
Binding to HTTPS using the iCDR directly is only recommended on Microsoft Windows Operating Systems. It is possible to bind the certificate to a port/address pair in Mono on Linux operating systems, however this feature is not widely documented.
{% endhint %}

{% hint style="info" %}
Consider using an TLS termination architecture for high-bandwidth deployments. Using a reverse proxy such as IIS or NGINX can greatly improve performance within the SanteDB iCDR environment as it allows shared web service endpoints to communicate using HTTP (with less overhead) whilst still allowing security transmission of data beyond the termination point.
{% endhint %}

