# HL7 Version 2 Service

The HL7 Version 2 Service configuration panel is used to enable or disable the sending and receiving of [HL7 Version 2.x](../../../../../operations-1/application-administration/santedb-administration-panel/security-administration/hl7v2.md) messages.

![](<../../../../../.gitbook/assets/image (432) (1) (1).png>)

| Setting                            | Description                                                                                                                                                                                                                                                                     | Example                                                                                                                                                    |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local Domain                       | The local assigning authority for the HL7 Version 2.x receiver. Whenever SanteDB encounters an identifier in this domain, it will assume the CX.1 refers to the UUID / key of the object.                                                                                       | See: [SanteDB HL7v2 Implementation](../../../../../developers/service-apis/hl7v2/santedb-hl7v2-implementation.md#internal-local-authority)                 |
| Authentication Mode                | Identifies the method of authenticating HL7 requests.                                                                                                                                                                                                                           | See: [SanteDB HL7v2 Authentication ](../../../../../developers/service-apis/hl7v2/hl7-authentication.md)notes.                                             |
| No Auth Secret                     | When not requiring application authentication, all values in the MSH-3 must be registered as a security application with this secret. This is the shared secret which the HL7 authentication layer uses to establish an application identity.                                   | `Fluffy_Penguins2`                                                                                                                                         |
| HL7 Services                       | Configuration for endpoints, messages, and trigger events for HL7 Services.                                                                                                                                                                                                     | See: [Service Endpoints](hl7-version-2-service.md#hl7-service-endpoints)                                                                                   |
| Receiving Facility ID              | The UUID of the local receiving facility for HL7v2 messages. The facility information is loaded from the primary data store based on this UUID and used to populate MSH-4 and MSH-5.                                                                                            | UUID                                                                                                                                                       |
| SSN Authority                      | The identity domain configuration for PID-19 (SSN). If using this field outside of the United States, this is the identity domain information for that field.                                                                                                                   | See: [SanteDB HL7v2 Implementation](../../../../../developers/service-apis/hl7v2/santedb-hl7v2-implementation.md#pid-19-social-security-resolution) notes. |
| Birthplace Types                   | A list of valid `ClassConcept` UUIDs which are used to resolve the PID birthplace. In HL7v2 birthplace is a plain string. This string is used to search for `Place` for a concrete birthplace relationship.                                                                     | UUID                                                                                                                                                       |
| Identifier Replacement             | When set to `AnyInDomain` , any attempt to update a patient identifier will remove the existing identifier for that patient in the domain and replace it with the provided value. This has the effect of only allowing one identifier per identity domain from a single sender. | `AnyInDomain`                                                                                                                                              |
| Strict Metadata                    | When set to TRUE any metadata in any field sent SanteDB must exactly match (place, organizations, etc.) must be matched exactly using the identifier in the XON rather than names.                                                                                              | `True` (recommended)                                                                                                                                       |
| Require Application Authentication | When true, all HL7 messages must be authenticated as Application + Device identity. When false, a Device Identity is used and the Application authentication comes from the `No Auth Secret` is used with MSH-3 to authenticate an application identity.                        | `True` (recommended)                                                                                                                                       |
| Strict CX4                         | When true resolution of CX.4 based on MSH values will be disabled and all senders MUST send CX4.1 or CX4.3                                                                                                                                                                      |                                                                                                                                                            |

## HL7 Service Endpoints

The HL7 Services configuration property allows administrators to edit one or more IP/Endpoints which can receive HL7v2 messages.

![](<../../../../../.gitbook/assets/image (435) (1) (1).png>)



| Setting          | Description                                                                                                                                   | Examples                                                                                                                             |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Endpoint         | The IP / port to listen for inbound messages for the services. 0.0.0.0 binds the endpoint to all IP addresses, 127.0.0.1 binds to localhost.  | <p>Unencrypted Localhost:</p><p><code>llp://127.0.0.1:2100</code></p><p>Encrypted Public:</p><p><code>sllp://0.0.0.0:2200</code></p> |
| Messages         | Messages (message types and trigger events) which can be processed on this endpoint.                                                          | See: [Messaging Events](hl7-version-2-service.md#messaging-events)                                                                   |
| Name             | The name of the endpoint which is shown in logs.                                                                                              | `My HL7 Endpoint`                                                                                                                    |
| Receive Timeout  | The number of milliseconds that the receiving endpoint will hold the connection open before forcably closing it.                              | `20000` (20 seconds)                                                                                                                 |
| Transport Option | When the endpoint uses `sllp://` as the endpoint binding, the transport binding options.                                                      | See: [Secure Endpoints](hl7-version-2-service.md#secure-endpoints)                                                                   |

### Secure Endpoints

When `sllp://` is used as the transport for the HL7 endpoint, the security settings for the endpoint.

![](<../../../../../.gitbook/assets/image (417) (1).png>)

| Setting                        | Description                                                                                                                                                                 | Examples                                                                                                  |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Check CRL                      | When true, the endpoint will attempt to check the Certificate Revocation List.                                                                                              | <p><code>False</code> - For faster performance</p><p><code>True</code> - For more secure transactions</p> |
| Enable Client Cert Negotiation | When true, the HL7 endpoint will challenge clients to provide a client certificate.                                                                                         | `True`                                                                                                    |
| Client CA Certificate          | The root certificate or intermediary certificate where client certificates must be bound to. The certificate chain will be validated against the this CA.                   | See: [Security Certificate](./#certificate-binding)                                                       |
| Server Certificate             | The certificate which the SanteDB iCDR will provide to clients which authenticates the server to clients. This certificate is also used to encrypt traffic with the client. | See: [Security Certificate](./#certificate-binding)                                                       |

### Messaging Events

Each HL7 endpoint can support multiple message / trigger events. The messages property of the endpoint specifies which message handlers can be used for which trigger events on the specified endpoint.

![](<../../../../../.gitbook/assets/image (424) (1) (1).png>)

| Setting         | Description                                                                                                                                    | Examples                                                      |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Message Handler | The implementation of the message handler which should be used to process messages which have any of the events listed in the events property. | ![](<../../../../../.gitbook/assets/image (433) (1) (1).png>) |
| Events          | The trigger events which should be forwarded to the selected message handler.                                                                  | `ADT^A01`                                                     |