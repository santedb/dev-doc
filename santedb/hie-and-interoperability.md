# HIE & Interoperability

SanteDB is designed with a variety interoperability interfaces and standards, including:

* HL7 Version 2.3 and Version 2.5 messaging
* HL7 FHIR 
* GS1 BMS 3.3
* IHE ATNA / UDP
* OpenID Connect Identity Provider
* OpenAPI / Swagger 2.0 Metadata Exchange

Each of these interfaces are enabled/disabled based on the role that SanteDB is operating in. For example, if SanteDB needs to act as an MPI then the GS1 and ATNA interfaces are disabled \(along with related user interface platforms\).

### Health Information Exchange Roles

SanteDB can be integrated into HIE architecture \(including OpenHIE\) in a variety of roles and should can be used to fill in missing functions. Some roles in which SanteDB can be configured.

<table>
  <thead>
    <tr>
      <th style="text-align:left">HIE Role</th>
      <th style="text-align:left">SanteDB Configuration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Client Registry</td>
      <td style="text-align:left">
        <ul>
          <li>SanteDB MDM Plugin</li>
          <li>SanteDB Matcher Plugin</li>
          <li>SanteDB FHIR Plugin (restricted down)</li>
          <li>SanteDB HL7 Plugin</li>
          <li>SanteMPI UI Plugin</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Shared Health Record</td>
      <td style="text-align:left">
        <ul>
          <li>SanteDB MDM Plugin (optional configured for apps)</li>
          <li>SanteDB FHIR Plugin</li>
          <li>SanteDB HL7 Plugin</li>
          <li>SanteDB GS1 BMS Plugin</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Audit Repository</td>
      <td style="text-align:left">
        <ul>
          <li>SanteDB FHIR Plugin</li>
          <li>SanteGuard Syslog Plugin</li>
          <li>SanteGuard Enhanced Audit Storage Plugin</li>
          <li>SanteGuard UI Plugin</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Facility Registry</td>
      <td style="text-align:left">
        <ul>
          <li>SanteDB MDM Plugin</li>
          <li>SanteDB Matcher Plugin</li>
          <li>SanteDB FHIR Plugin</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Product Registry</td>
      <td style="text-align:left">
        <ul>
          <li>SanteDB MDM Plugin</li>
          <li>SanteDB Matcher Plugin</li>
          <li>SanteDB FHIR Plugin</li>
          <li>SanteDB GS1 Plugin</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Identity Provider / User Registry</td>
      <td style="text-align:left">
        <ul>
          <li>SanteDB OAUTH / OpenID Plugins</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
While SanteDB can be integrated into OpenHIE, it doesn't require a full OpenHIE infrastructure to operate properly. It can be used as a launch point into a broader e-health strategy.
{% endhint %}

### Roadmap

There are additional product features which have been identified as part of the SanteDB roadmap which would facilitate leveraging SanteDB in other future roles.

* XACML Interface - The SanteDB internal policy framework was modeled after the patterns defined in XACML \(PEP, PDP, PIP\).
* HL7v3 & IHE PIX/PDQv3 - The SanteDB database is primarily based on concepts from the HL7 RIM which HL7v3 is also based on this infrastructure, implementation of the v3 interfaces can be implemented.
* IHE XDS and SVS Interface - To properly support being in consent directive management service the service should accept BPPC consent documents.

