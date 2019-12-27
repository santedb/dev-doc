# Parameters

Parameter definitions allow you to define common, reusable parameters within SanteDB. The default parameter definitions provided by SanteDB are:

| ID | Type | Description |
| :--- | :--- | :--- |
| org.santedb.bi.core.parameter.common.date.from | DATE | A date-picker input which has a max value of to-date. |
| org.santedb.bi.core.parameter.common.date.to | DATE | A date picker input which has a min value of from-date |
| org.santedb.bi.core.parameter.user.class | UUID | User class parameters. |

### Parameter Definition Files

Parameter definitions are used to provide common input controls to reports and queries. These parameters, like data sources can also be annotated with metadata including permission directives.

```markup
<BiParameterDefinition xmlns="http://santedb.org/bi" 
  id="org.custom.parameter.referenceType" 
  name="reference_data_version" 
  label="Reference Version" 
  type="string" 
  default="2.0">
  <meta status="active">
    <authors>
      <add>Sample Organization</add>
    </authors>
    <annotation lang="en">
      <div xmlns="http://www.w3.org/1999/xhtml">
        <p>This parameter controls all reference queries to restrict to version</p>
      </div>
    </annotation>
  </meta>
  <values>
    <add value="2.0">Version 2.0 (May 2019)</add>
    <add value="1.1">Version 1.1 (Sept 2018)</add>
    <add value="1.0">Version 1.0 (Oct 2017)</add>
  </values>
</BiParameterDefinition>
```

This particular parameter definition represents a drop-down list with a fixed number of options. Alternately you can specify a query source for this:

```markup
<BiParameterDefinition xmlns="http://santedb.org/bi" 
   ...>
  <meta status="active"> 
     ...
  </meta>
  <query>
    <dataSources>
      <add ref="#org.custom.dataSource.references" name="main"/>
    </dataSources>
    <definitions>
      <add>
        <providers>
          <invariant>PSQL</invariant>
          <invariant>FBSQL</invariant>
        </providers>
        <![CDATA[SELECT DISTINCT id, name FROM versions]]>
      </add>
    </definitions>
  </query>
</BiParmaeterDefinition>
```

{% hint style="info" %}
In the BI engine you can include any data inline, or you can reference it by ID . In the example above, one could define a query with ID org.custom.query.version and reference it from their parameter definition as:

```markup
 <query ref="#org.custom.query.version"/>
```
{% endhint %}

### 

