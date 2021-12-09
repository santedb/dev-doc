# Auditing Configuration

SanteDB iCDR carries two different auditing technologies in the default installation:

* ATNA Auditing - Which is performed over UDP or TCP with NEMA DICOM or IETF RFC3881 formatted audits. This is recommended for high traffic environments at is has little overhead.
* FHIR Auditing - Which is performed over HTTP with FHIR audit event resources.

You can only enable one audit dispatcher (FHIR OR ATNA , if you enable one the other will be disabled).

## ATNA Audit Dispatching

The ATNA auditing dispatch service, when enabled, will ensure that SanteDB forwards audits for events which are to be dispatched over UDP.

![](<../../../../.gitbook/assets/image (423) (1) (1).png>)

| Option             | Description                                                                                                                                                           | Example                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Endpoint           | The IP address or host name and port to send audit messages to.                                                                                                       | `localhost:11514`                                                                           |
| Transport          | The transport which should be used to send audits. All audits are sent on SYSLOG, this controls the transport mechanism for SYSLOG.                                   | <p>Tcp = SYSLOG over TCP</p><p>Stcp = SYSLOG over TCP + TLS</p><p>UDP = SYSLOG Over UDP</p> |
| Enterprise Site    |  The enterprise site identifier to use in the audit messages sent to the remote endpoint. Used to identify the logical group of SanteDB servers this iCDR belongs to. |                                                                                             |
| Client Certificate | When using STCP, the client certificate to present to the server to authenticate the local node. Your node must have the private key for this certificate.            | See: [Certificate Binding](../messaging-settings/#certificate-binding)                      |
| Server Certificate | When using STCP the public key which is expected from the server.                                                                                                     |                                                                                             |
| Format             | The format of audits that the remote endpoint is expecting.                                                                                                           | <p>DICOM - Use NEMA Dicom Format</p><p>RFC3881 - Use IETF RFC881 Format</p>                 |
