# HL7 Version 2 Service

The HL7 Version 2 Service configuration panel is used to enable or disable the sending and receiving of [HL7 Version 2.x](../../../../extending-santedb/service-apis/hl7v2/) messages.

![](<../../../../../.gitbook/assets/image (432).png>)

| Setting                            | Description                                                                                                                                                                                                                                                                                                                           | Values                 |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| Local Domain                       | The local assigning authority for the HL7 Version 2.x receiver. Whenever SanteDB encounters an identifier in this domain, it will assume the CX.1 refers to the UUID / key of the object. See [SanteDB HL7v2 Implementation](../../../../extending-santedb/service-apis/hl7v2/santedb-hl7v2-implementation/#internal-local-authority) | Assigning Authority    |
| Authentication Mode                | Identifies the method of authenticating HL7 requests. See [SanteDB HL7v2 Authentication ](../../../../extending-santedb/service-apis/hl7v2/santedb-hl7v2-implementation/hl7-authentication.md)notes.                                                                                                                                  | MSH8 / SFT4 / NONE     |
| HL7 Services                       | Configuration for endpoints, messages, and trigger events for HL7 Services.                                                                                                                                                                                                                                                           | See Below              |
| Receiving Facility ID              | The UUID of the local receiving facility for HL7v2 messages. The facility information is loaded from the primary data store based on this UUID and used to populate MSH-4 and MSH-5.                                                                                                                                                  | UUID                   |
| SSN Authority                      | The identity domain configuration for PID-19 (SSN). If using this field outside of the United States, this is the identity domain information for that field. See [SanteDB HL7v2 Implementation](../../../../extending-santedb/service-apis/hl7v2/santedb-hl7v2-implementation/#pid-19-social-security-resolution) notes.             | Assigning Authority    |
| Birthplace Types                   | A list of valid `ClassConcept` UUIDs which are used to resolve the PID birthplace. In HL7v2 birthplace is a plain string. This string is used to search for `Place` for a concrete birthplace relationship.                                                                                                                           | UUID                   |
| Identifier Replacement             | When set to `AnyInDomain` , any attempt to update a patient identifier will remove the existing identifier for that patient in the domain and replace it with the provided value. This has the effect of only allowing one identifier per identity domain from a single sender.                                                       | AnyInDomain / Specific |
| Strict Metadata                    | When set to TRUE any metadata in any field sent SanteDB must exactly match (place, organizations, etc.) must be matched exactly using the identifier in the XON rather than names.                                                                                                                                                    |                        |
| Require Application Authentication | When true, all HL7 messages must be authenticated as Application + Device identity. When false, a Device Identity is used and the Application authentication comes from the `No Auth Secret` is used with MSH-3 to authenticate an application identity.                                                                              |                        |
| Strict CX4                         | When true resolution of CX.4 based on MSH values will be disabled and all senders MUST send CX4.1 or CX4.3                                                                                                                                                                                                                            |                        |

## HL7 Service Endpoints

The HL7 Services configuration property allows administrators to edit one or more IP/Endpoints which can receive HL7v2 messages.

![](<../../../../../.gitbook/assets/image (435) (1).png>)



| Setting          | Description                                                                                                                                   | Values                                                                                |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Endpoint         | The IP / port to listen for inbound messages for the services. 0.0.0.0 binds the endpoint to all IP addresses, 127.0.0.1 binds to localhost.  | <p>llp:// -> Unencrypted</p><p>sllp:// -> Encrypted</p><p>tcp:// -> Plain sockets</p> |
| Messages         | Messages (message types and trigger events) which can be processed on this endpoint.                                                          |                                                                                       |
| Name             | The name of the endpoint which is shown in logs.                                                                                              |                                                                                       |
| Receive Timeout  | The number of milliseconds that the receiving endpoint will hold the connection open before forcably closing it.                              |                                                                                       |
| Transport Option | When the endpoint uses `sllp://` as the endpoint binding, the transport binding options.                                                      |                                                                                       |

### Secure Endpoints

When `sllp://` is used as the transport for the HL7 endpoint, the security settings for the endpoint.

![](<../../../../../.gitbook/assets/image (417).png>)

| Setting                        | Description                                                                                                                                                                 | Values                                                          |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Check CRL                      | When true, the endpoint will attempt to check the Certificate Revocation List.                                                                                              | Boolean                                                         |
| Enable Client Cert Negotiation | When true, the HL7 endpoint will challenge clients to provide a client certificate.                                                                                         | Boolean                                                         |
| Client CA Certificate          | The root certificate or intermediary certificate where client certificates must be bound to. The certificate chain will be validated against the this CA.                   | See: [Security Certificate](../messaging-settings.md#endpoints) |
| Server Certificate             | The certificate which the SanteDB iCDR will provide to clients which authenticates the server to clients. This certificate is also used to encrypt traffic with the client. | See: [Security Certificate](../messaging-settings.md#endpoints) |

### Messaging Events

Each HL7 endpoint can support multiple message / trigger events. The messages property of the endpoint specifies which message handlers can be used for which trigger events on the specified endpoint.

![](<../../../../../.gitbook/assets/image (424).png>)

| Setting         | Description                                                                                                                                    | Values                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Message Handler | The implementation of the message handler which should be used to process messages which have any of the events listed in the events property. | ![](<../../../../../.gitbook/assets/image (433).png>) |
| Events          | The trigger events which should be forwarded to the selected message handler.                                                                  |                                                       |
