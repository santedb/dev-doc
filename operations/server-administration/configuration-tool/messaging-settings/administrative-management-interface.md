# Administrative Management Interface

The administrative management interface configuration provides two configuration properties.

![](<../../../../.gitbook/assets/image (422) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

| Setting          | Description                                                                                                                                                                                                                                                         | Values |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| CA Configuration | <p>Configuration when using the SanteDB Certificate Authority services.</p><p>Note: This setting is being refactored to a more portable solution using BouncyCastle for certificate management. It is recommended you do not use this functionality in SanteDB </p> |        |
| API Endpoints    | If the iCDR is being used in a distributed environment - you can use this setting to specify the other servers in your iCDR cluster. The service discovery on the AMI will point clients to the appropriate endpoints.                                              |        |

### API Endpoints and Clustering

When you cluster your iCDR service, you can opt to have a single application server (or server group) take on an individual roles in the SanteDB iCDR infrastructure. The dCDR, however, will use the AMI on the primary server to discover alternate locations and services in the deployment.

When running SanteDB iCDR on a single server, the API Endpoints configuration should not be used, as the server auto-detects its environment. However, when using the iCDR on multiple servers you should configure the primary iCDR to point to the other servers in your cluster.

![](<../../../../.gitbook/assets/image (428) (1) (1) (1) (1) (1).png>)

| Setting          | Description                                                                                                                                                                           | Values                                                                                                                                                                                                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Capabilities     | The capabilities of the remote service. These are used by dCDR clients when discovering the iCDR environment to determine whether compression, CORS or other behaviors are supported. | <p>StandardsApi -> The API is a Standards-based-API with no special capabilities</p><p>InternalApi -> The API is a proprietary API which supports extensions for SanteDB like compression and CORS</p><p>StandardsBasedCorsAPI-> Standards based API with CORS enabled.</p> |
| Service Behavior | The type of service which is running on the remote endpoint. This is used by the AMI and OpenAPI endpoint to reflect methods and expected responses.                                  |                                                                                                                                                                                                                                                                             |
| Service Type     | The classification of the service. This allows the remote endpoint to know whether the service is an AMI, HDSI, FHIR, HL7 or other endpoint.                                          |                                                                                                                                                                                                                                                                             |
| Service URL(s)   | A list of publicly accessible URLs where the remote service can be accessed by dCDR clients.                                                                                          |                                                                                                                                                                                                                                                                             |
