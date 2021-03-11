# Data Quality Services

SanteDB iCDR and dCDR have the ability to execute data quality and validation rules whenever data is presented to the iCDR regardless of the source of the data \(such as FHIR, UI, HL7v2 interfaces, etc.\).

The data quality service listens for events at the repository layer, runs the validation rules, and then flags any data quality issues using the `http://santedb.org/extensions/detected-issue` extension. Uses for this service are:

* Allowing the assertion of data quality rules whereby data can be persisted \(not rejected\) for later reconciliation
* Allowing the rejection of inbound data \(if the quality rule issues an Error\)
* Allowing the matching algorithm to ignore records which have particular data quality issues.

## Registering the Data Quality Service

To enable the data quality service, you should add the following service definition to your application service configuration section.

```markup
  <section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="8">
    <serviceProviders>
       ...
       <add type="SanteDB.Core.Data.Quality.DataQualityService, SanteDB.Core.Api, Version=2.1.0.0"/>
       ...
     </serviceProviders>
   </section>
```

## Configuring Data Quality Rules

Data quality rules are configured using the `DataQualityConfigurationSection` identified in `SanteDB.Core.Data.Quality.Configuration.DataQualityConfigurationSection, SanteDB.Core.Api, Version=2.1.0.0`

The data quality configuration section comprises of one or more rulesets which define the validation rules to be applied to incoming data. Rule sets are expressed on the data quality extension, by identifier of the rule. For example, to create a data quality ruleset which validates that date of birth is provided on a patient and that name is provided for Place objects:

```markup
  <!-- Data Quality Configuration Section -->
  <section xsi:type="DataQualityConfigurationSection">
    <!-- Rule Set for data quality -->
    <ruleSet enabled="true" id="my-rule-set" name="My Data Quality Configuration">
      <resources>
        <add resource="Patient">
          <assert id="dob.required" name="Date of Birth Required" priority="Warning">
            <expression>dateOfBirth=!null</expression>
          </assert>
        </add>
        <add resource="Place">
          <assert id="name.required" name="Name Required" priority="Error">
            <expression>name.component.value=!null</expression>
          </assert>
      </resources>
    </ruleSet>
  </section>
```

### Assertions

The assertions made within the rule set identify the HDSI Query syntax. The structure of assertions are:

```markup
<assert id="unique-identifier" name="What Is Shown To Users" priority="Informational|Warning|Error">
          <expression>ASSERTION_WHEN_TRUE</expression>
</assert>
```

If any one of the &lt;expression&gt; element expression evaluate to FALSE then the assertion is considered failed, and the id is emitted to the detected issue extension. When an assertion has a priority of ERROR then the entire transaction is aborted and the rules are emitted on the API \(response code 422\).



