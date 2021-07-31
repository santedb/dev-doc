# Enabling HL7v2 Interfaces

To enable the HL7v2 messaging interfaces, the SanteDB iCDR host instance's configuration file needs to be updated to include the `HL7ConfigurationSection` as illustrated:

```markup
<SanteDBConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://santedb.org/configuration">
  <sections>
    <add type="SanteDB.Messaging.HL7.Configuration.Hl7ConfigurationSection, SanteDB.Messaging.HL7" />
  </sections>
  <section xsi:type="Hl7ConfigurationSection" 
          strictMetadata="false" requireAppAuth="false" 
          idReplacement="any-in-domain"  security="None">
    <!-- Classes of PLACE which can be used for a Birthplace Lookup -->
    <birthplaceClasses>
      <add>79DD4F75-68E8-4722-A7F5-8BC2E08F5CD6</add>
      <add>48B2FFB3-07DB-47BA-AD73-FC8FB8502471</add>
      <add>D9489D56-DDAC-4596-B5C6-8F41D73D8DC5</add>
      <add>FF34DFA7-C6D3-4F8B-BC9F-14BCDC13BA6C</add>
      <add>8CF4B0B0-84E5-4122-85FE-6AFA8240C218</add>
    </birthplaceClasses>
    <!-- The UUID of your local facility -->
    <facility>84039432-84E5-4122-85FE-6AFA8240C218</facility>
    <!-- The authority of your UUIDs -->
    <localAuthority>
      <domainName xmlns="http://santedb.org/model">YOUR_LOCAL_V2_AUTHORITY</domainName>
      <oid xmlns="http://santedb.org/model">1.3.6.1.4.1.52820.5.1.1.1.999</oid>
      <url xmlns="http://santedb.org/model">http://your/fhir/authority</url>
    </localAuthority>
    <!-- The SSN Authority from PID segment (map to PID-3) -->
    <ssnAuthority>
      <domainName xmlns="http://santedb.org/model">SSN</domainName>
      <oid xmlns="http://santedb.org/model">2.16.840.1.113883.4.1</oid>
      <url xmlns="http://santedb.org/model">http://hl7.org/fhir/sid/us-ssn</url>
    </ssnAuthority>
    <services>
      <!-- One or more IP/PORTS on which to bind -->
      <add address="llp://0.0.0.0:2100" name="LLP" receiveTimeout="20000">
        <!-- If you want to enable security Encryption
        <sllp checkCrl="false" requireClientCert="false">
          <serverCertificate findType="FindByThumbprint" storeName="My" storeLocation="CurrentUser" findValue="value" />
          <clientAuthorityCertificate findType="FindByThumbprint" storeName="My" storeLocation="CurrentUser" findValue="value" />
        </sllp>
        -->
        <handler>
          <add type="SanteDB.Messaging.HL7.Messages.QbpMessageHandler, SanteDB.Messaging.HL7, Version=1.10.0.0">
            <message isQuery="true" name="QBP^Q22" />
            <message isQuery="true" name="QBP^Q23" />
          </add>
          <add type="SanteDB.Messaging.HL7.Messages.AdtMessageHandler, SanteDB.Messaging.HL7, Version=1.10.0.0">
            <message isQuery="false" name="ADT^A01"/>
            <message isQuery="false" name="ADT^A04"/>
            <message isQuery="false" name="ADT^A08"/>
            <message isQuery="false" name="ADT^A40"/>
          </add>
        </handler>
      </add>
    </services>
  </section>

</SanteDBConfiguration>
```

## Security Configuration

### Anonymous User

If SanteDB is used in a context where SLLP is not used to authenticate devices, and senders do not support MSH-8 then you can set the authentication mode to none and set the `@anonUser` attribute. This attribute is the anonymous user account that you wish unauthenticated contexts to run under. By default, `ANONYMOUS` is used.

### Authentication Method

The `@security` attribute can have one of the values drawn from the list below, which impact the method with which clients are authenticated:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Behavior</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">None</td>
      <td style="text-align:left">No special authentication is performed, if communicating with SLLP and
        client certificates then the <code>DevicePrincipal</code> is established
        via the client certificate. Otherwise the <code>@anonUser</code> value is
        used as authentication.</td>
    </tr>
    <tr>
      <td style="text-align:left">Msh8</td>
      <td style="text-align:left">
        <p>The value of <code>MSH-3|MSH-4</code> is used as the device identity and
          the value of <code>MSH-8</code> is used to authenticate a device if not on
          SLLP, the value of <code>MSH-3</code> and <code>MSH-8</code> is used to authenticate
          the application if <code>@requireAppAuth</code> is set to true.</p>
        <p>If the message was received on SLLP then the client certificate is used
          to authenticate the sender.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Sft4</td>
      <td style="text-align:left">The value of <code>MSH-3|MSH-4</code> is used to authenticate the device
        if non-SLLP transport was used, and the value of <code>SFT-2</code> and <code>SFT-4</code> are
        used to authenticate the application. If the message was received on SLLP
        then the client certificate is used to authenticate the sender.</td>
    </tr>
  </tbody>
</table>

## Metadata / Control Configuration

The elements which control metadata used by the HL7 message handler are:

| Element | Use |
| :--- | :--- |
| `@strictMetadata` | When true, segment processing must only assign relationships \(to organizations, facilities, etc.\) when an explicit identifier matches that registered in the CDR. If false, then the segment handler will attempt name matching of places to perform linking. |
| `@idReplacement` | When set to `any-in-domain` , any attempt to update a patient identifier will remove the existing identifier for that patient in the domain and replace it with the provided value. This has the effect of only allowing one identifier per identity domain from a single sender. |
| `birthplaceClasses` | In HL7v2, the birthplace of patients and persons are represented as simple place names. This list provides a series of class codes which `Place` instances can have to resolve to a birthplace. For example, one can enable `SerivceDeliveryLocation` as a class code for birthplace and SanteDB will match birthplaces with hospitals and clinics. |
| `facility` | This is the value of the `ServiceDeliveryLocation` instance in which the instance of SanteDB is running. This information is used to populate the `MSH-4` field if the iCDR is sending HL7 messages, or the `MSH-6` field if matching inbound messages. |
| `localAuthority` | Contains an `AssigningAuthority` which is used to emit local keys and designate inbound identifiers as a local identifier. Given the example above, the internal resource UUID for a patient would be emitted in HL7 as: `9ce06884-39ff-42b6-87b4-bd6b9df24702^^^YOUR_LOCAL_V2_AUTHORITY&1.3.6.1.4.1.52820.5.1.1.1.999&ISO` |
| `ssnAuthority` | Like the `localAuthority` , this contains the domain which the `PID-19` field should be mapped to \(since SanteDB's HL7 handler maps this into a `PID-3` identity domain\) |

## HL7 Services

The message handler can expose one or more endpoints with different message handler and port bindings based on the requirements of the environment in which SanteDB is deployed. Each service defines a `address` attribute which is a URI on which the service should be bound. The schemes for this URI are:

| Scheme | Transport | Example |
| :--- | :--- | :--- |
| llp | HL7 Lower Layer Protocol \(not encrypted\) | llp://0.0.0.0:2100/ |
| tcp | Raw TCP/IP Sockets | tcp://127.0.0.1:9990/ |
| sllp | HL7 Lower Layer Protocol + TLS Transport | sllp://0.0.0.0:2100/ |

Each service also requires the definition for which trigger events and which handlers should be used on that particular service endpoint which are configured using the `<handler>` element. 

### TLS + LLP \(SLLP\) 

When using the TLS option, you must provide an `<sllp>` element, which controls how the encryption for the channel is setup.

| Element / Attribute | Description |
| :--- | :--- |
| `@checkCrl` | When true, instructs the iCDR to actively check the listed CRL on the certificate to validate whether the certificate is revoked. When enabled, there may be a performance penalty since the CRL cache on some operating systems is not present in .NET. |
| `@requireClientCert` | When true, instructs the iCDR to challenge clients for a client certificate for node authentication.  |
| `serverCertificate` | Specifies the manner in which the X.509 certificate for encrypting server traffic should be located. This is the certificate which the iCDR will use to authenticate itself to clients and encrypt traffic. The certificate find mechanism uses the Windows certificate store \(on Windows\) or the Mono certificate tool \(on Linux or Mac\) |
| `clientAuthorityCertificate` | Specifies the certification authority root which is used to validate clients are permitted to access the server. This certificate should appear in the client certificate's chain, or else validation fails. Note: This is a pre-check, actual device principals are created using the certificate thumbprint and the `MSH` segment. |

