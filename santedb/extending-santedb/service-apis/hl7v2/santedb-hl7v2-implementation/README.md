# SanteDB HL7v2 Implementation

Any implementation of HL7 Version 2 messaging has its own method of processing messages, and SanteDB is no different. This page discusses the particulars of the SanteDB's implementation of the HL7v2 message specification.

## Version Support

SanteDB uses HL7 Version 2.5 as its internal canonical model for HL7 messages. All services in SanteDB's HL7 layer are implemented using Version 2.5 structures, and wire versions are translated to/from that version.

Because of this implementation, HL7v2.5 is the latest version of messaging supported by SanteDB. 

## Transport Support

SanteDB supports common HL7 Version 2.5 transports including:

* TCP Sockets -&gt; Raw messages sent over a simple TCP socket, containing no special control characters.
* Lower Layer Protocol -&gt; Unsecured TCP socket which uses the LLP control characters \(VT, FS, CR, etc.\) for delineation of message boundaries.
* Secure Lower Layer Protocol -&gt;  A TLS wrapped TCP socket which uses the LLP control characters. This transport also supports client authentication.

Each service in the HL7 message handler defines an `address` attribute which has a URI. The scheme of this URI dictates the selected transport for messaging. The schemes for this URI are:

| Scheme | Transport | Example |
| :--- | :--- | :--- |
| llp | HL7 Lower Layer Protocol \(not encrypted\) | llp://0.0.0.0:2100/ |
| tcp | Raw TCP/IP Sockets | tcp://127.0.0.1:9990/ |
| sllp | HL7 Lower Layer Protocol + TLS Transport | sllp://0.0.0.0:2100/ |

Each service also requires the definition for which trigger events and which handlers should be used on that particular service endpoint which are configured using the `<handler>` element. 

### TLS + LLP \(SLLP\) 

When using the TLS option, you must provide an `<sllp>` element, which controls how the encryption for the channel is setup.

A simple encrypted channel over SLLP where no client authentication is required is configured as:

```markup
 <add address="sllp://0.0.0.0:2200" receiveTimeout="0" name="SanteMPI IHE SLLP">
  <sllp checkCrl="true" requireClientCert="false">
    <serverCertificate findType="FindByThumbprint" storeLocation="LocalMachine" findValue="467808134ADFFA873694261C707016EC03080A86" />
  </sllp>
  
```

| Element / Attribute | Description |
| :--- | :--- |
| `@checkCrl` | When true, instructs the iCDR to actively check the listed CRL on the certificate to validate whether the certificate is revoked. When enabled, there may be a performance penalty since the CRL cache on some operating systems is not present in .NET. |
| `@requireClientCert` | When true, instructs the iCDR to challenge clients for a client certificate for node authentication.  |
| `serverCertificate` | Specifies the manner in which the X.509 certificate for encrypting server traffic should be located. This is the certificate which the iCDR will use to authenticate itself to clients and encrypt traffic. The certificate find mechanism uses the Windows certificate store \(on Windows\) or the Mono certificate tool \(on Linux or Mac\) |
| `clientAuthorityCertificate` | Specifies the certification authority root which is used to validate clients are permitted to access the server. This certificate should appear in the client certificate's chain, or else validation fails. Note: This is a pre-check, actual device principals are created using the certificate thumbprint and the `MSH` segment. |

## Identity Domain / Assigning Authority Resolution

Within an HL7 message, identifiers using the `CX` datatype \(composite identifier\) carry an fourth component which indicates the authority under which the identity was assigned. 

### Simple Namespace

Whenever the `CX.4` component carry a simple value such as: `304-304-203^^^SSN` the namespace ID is mapped to the `DomainName` property of an assigning authority. In this case, SanteDB would search its data store for a configured assigning authority with `DomainName` of SSN.

### Universal Namespace

Whenever the `CX.4` component carries a universal identifier, such as : `304-304-203^^^&2.16.840.1.113883.4.1&ISO` the SanteDB server will map the `CX.4.2` to the `Oid` property of the assigning authority. 

{% hint style="info" %}
When using both a NamespaceID and a UniversalID , for example: `304-304-203^^^SSN&2.16.840.1.113883.4.1&ISO` then SanteDB will ensure that both components agree on the authority to be resolved.
{% endhint %}

### No Namespace

Some older PACS systems do not include clearly specified identity domains in the `CX.4` ,  for example, if a sender issues a request such as:

```text
MSH|^~\&|PACS|CENTRAL|CR1|MOH_CAAT|20211104174451||ADT^A01^ADT_A01||P|2.3.1
EVN||20101020
PID|||RJ-438||JOHNSTON^BOB^^^^^L
PV1||I
```

The SanteDB instance must attempt to resolve the authority under which `RJ-438` is registered. To do this, the SanteDB server will attempt to locate any assigning authority which the authenticated application principal is permitted to assign. In this case the assigning application would be `PACS` . If more than one candidate authority is located, then a `CR` indicating ambiguous authorities were found.

{% hint style="info" %}
In order for no namespace resolution to be enabled, the value of `strictCx4` in the configuration must be set to `false`
{% endhint %}

### PID-19 / Social Security Resolution

If your deployment uses the `PID-19` field to convey a national social security number, you must configure the `ssnAuthority` element in your HL7 configuration which links the SSN authority with a registered identity domain. For example, in the US to configure `PID-19` to use the built-in SSN authority name:

```markup
<ssnAuthority operation="Auto">
    <domainName xmlns="http://santedb.org/model">SSN</domainName>
    <oid xmlns="http://santedb.org/model">2.16.840.1.113883.4.1</oid>
    <url xmlns="http://santedb.org/model">http://hl7.org/fhir/sid/us-ssn</url>
</ssnAuthority>
```

This will allow the resolution of the simple string in `PID-19` to map to an authority. 

{% hint style="info" %}
If your deployment uses `PID-19` to map to another identity such as national social insurance number, etc. you should modify the `ssnAuthority` element to match.
{% endhint %}

### Internal / Local Authority

When SanteDB responds or receives a message in HL7v2, it is possible to reference the UUID for the object using the `PID-3` segment if the `localAuthority` element is configured.

```text
<localAuthority operation="Auto">
    <domainName xmlns="http://santedb.org/model">LOCAL_AUTH</domainName>
    <oid xmlns="http://santedb.org/model">1.3.6.1.4.1.52820.5.1.1.1.999</oid>
    <url xmlns="http://santedb.org/model">http://your/fhir/authority</url>
</localAuthority>
```

For example, to allow a client to explicitly merge two discrete records \(known UUIDS\) on the SanteDB server, with the configuration above, the source system would send:

```text
MSH|^~\&|PACS|CENTRAL|CR1|MOH_CAAT|20211104174451||ADT^A40^ADT_A40||P|2.3.1
EVN||20101020
PID|||5634a7a3-a394-4010-8681-34adff13a47e^^^LOCAL_AUTH||JOHNSTON^BOB^^^^^L
MRG|2f4b0ac1-6edb-4b16-9d4d-339b2455f66e^^^LOCAL_AUTH
```

