# FHIR R4 Service

The FHIR R4 configuration panel is used to control the configuration of the [FHIR API ](../../../../../operations-1/standard-operating-procedures/hl7-fhir/)endpoint.

![](<../../../../../.gitbook/assets/image (423) (1) (1).png>)

| Setting               | Description                                                                                                                                                                                                                                                                                                                                                                   | Examples                                                      |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| REST API Service Name | The name of the REST API service the FHIR interface should bind to. The default is FHIR however if you change the REST API name (in the panel section above) you should also change the name here.                                                                                                                                                                            | `FHIR`                                                        |
| Landing Page          | The HTML page where the FHIR service should use when a user accesses the FHIR base URL with no specific request.                                                                                                                                                                                                                                                              | `C:\foo\index.html`                                           |
| Resource Handlers     | When configured, the allowed resources which can be used on the FHIR server. If not set, then the FHIR handler will enable all installed resources on the server. This setting allows the administrator to reduce the number of resources which can be used.                                                                                                                  | ![](<../../../../../.gitbook/assets/image (418).png>)         |
| Operation Handlers    | When configured, the allowed operations (via `$operation`) on the FHIR API endpoints. When not set, the FHIR service will enable all operation handlers installed.                                                                                                                                                                                                            | ![](<../../../../../.gitbook/assets/image (420) (1) (1).png>) |
| Message Handlers      | When configured, the allowed FHIR messages on the API endpoints (via `$process-message`). When not set, the FHIR API will expose all message handlers installed on the SanteDB server.                                                                                                                                                                                        | ![](<../../../../../.gitbook/assets/image (419) (1).png>)     |
| Extension Handlers    | <p>When configured, the extensions which are permitted to be used on the FHIR server. When disabled, the SanteDB FHIR API will enable all FHIR extensions.</p><p>Note: When an extension handler is disabled, it merely disables special treatment of that extension - the extensions being received will be placed into the <code>Extensions</code> property of the RIM.</p> | ![](<../../../../../.gitbook/assets/image (431) (1) (1).png>) |
| Profile Handlers      | When configured, the special profile validation services which should be used on the FHIR API.                                                                                                                                                                                                                                                                                |                                                               |
| Behavior Modifiers    | When configured, the behavior modifiers for the FHIR service. Behavior modifiers allow the FHIR API to implement specific standards-based behaviors on the FHIR service.                                                                                                                                                                                                      | ![](<../../../../../.gitbook/assets/image (430) (1) (1).png>) |
| Base Operation URL    | The URL to expose to clients when a `Conformance` request or `StructureDefinition` request is received or when representing a full URL for a resource. This should be the publicly accessible URL for the FHIR service.                                                                                                                                                       | `https://public.com/fhir`                                     |
| Default Format        | The default format for FHIR requests.                                                                                                                                                                                                                                                                                                                                         | JSON / XML                                                    |