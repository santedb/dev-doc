# Administrative Management Interface

The administrative management interface configuration provides two configuration properties.

![](<../../../../.gitbook/assets/image (99).png>)

<table><thead><tr><th width="216.2676612932232">Setting</th><th width="269.5026452105254">Description</th><th>Values</th></tr></thead><tbody><tr><td>CA Configuration</td><td><p>Configuration when using the SanteDB Certificate Authority services.</p><p>Note: This setting is being refactored to a more portable solution using BouncyCastle for certificate management. It is recommended you do not use this functionality in SanteDB </p></td><td></td></tr><tr><td>API Endpoints</td><td>If the iCDR is being used in a distributed environment - you can use this setting to specify the other servers in your iCDR cluster. The service discovery on the AMI will point clients to the appropriate endpoints.</td><td></td></tr></tbody></table>

### API Endpoints and Clustering

When you cluster your iCDR service, you can opt to have a single application server (or server group) take on an individual roles in the SanteDB iCDR infrastructure. The dCDR, however, will use the AMI on the primary server to discover alternate locations and services in the deployment.

When running SanteDB iCDR on a single server, the API Endpoints configuration should not be used, as the server auto-detects its environment. However, when using the iCDR on multiple servers you should configure the primary iCDR to point to the other servers in your cluster.

![](<../../../../.gitbook/assets/image (446).png>)

<table><thead><tr><th width="207.89270213822925">Setting</th><th width="269.5026452105254">Description</th><th>Values</th></tr></thead><tbody><tr><td>Capabilities</td><td>The capabilities of the remote service. These are used by dCDR clients when discovering the iCDR environment to determine whether compression, CORS or other behaviors are supported.</td><td><p>StandardsApi -> The API is a Standards-based-API with no special capabilities</p><p>InternalApi -> The API is a proprietary API which supports extensions for SanteDB like compression and CORS</p><p>StandardsBasedCorsAPI-> Standards based API with CORS enabled.</p></td></tr><tr><td>Service Behavior</td><td>The type of service which is running on the remote endpoint. This is used by the AMI and OpenAPI endpoint to reflect methods and expected responses.</td><td></td></tr><tr><td>Service Type</td><td>The classification of the service. This allows the remote endpoint to know whether the service is an AMI, HDSI, FHIR, HL7 or other endpoint.</td><td></td></tr><tr><td>Service URL(s)</td><td>A list of publicly accessible URLs where the remote service can be accessed by dCDR clients.</td><td></td></tr></tbody></table>
