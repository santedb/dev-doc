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



