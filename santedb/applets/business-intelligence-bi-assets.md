# Business Intelligence \(BI\) Assets

SanteDB supports the generation of reports and fetching of aggregate data for charting and business intelligence functions \(such as FHIR MeasureReport resources\)  using the BI infrastructure. BI assets are defined in the /bi folder of your applet and can contain:

* BiPackages - A collection of BI assets for a particular purpose \(for example: a custom report including parameters and queries\)
* BiDataSource - Defines a connection to a particular data source such as relational data or custom IBiDataProvider instance written in .NET.
* BiParameterDefinitions - Defines a reusable parameter for use in queries and reports. Parameter definitions define the type, validation, and data source \(lists\) for inputs into queries.
* BiQueryDefinition - Defines a common query against one or more data sources \(example: master patient list\)
* BiViewDefinition - Defines a view on top of a BiQueryDefinition. This allows for data source independent aggregation and pivoting of results.
* BiReportDefinition - Defines a user friendly view of data defined in a view.

All BI assets are defined in XML in the **http://santedb.org/bi** namespace. The schema for this namespace is in the Schema\ directory of your SanteDB installation.

### Data Sources

BI Data Sources represent the source for data where queries are executed. A data source can be a relational data store \(such as a data store used by SanteDB infrastructure\) or an external data source \(such as a website, API, or reference data sets\).

Data sources are defined using XML. Data sources must also provide a IBiDataSource implementation. For example, to define a reference data source using PostgreSQL one would use:

```markup
<BiDataSourceDefinition name="references" id="org.custom.dataSource.references" 
   provider="SanteDB.OrmLite.OrmBiDataProvider, SanteDB.OrmLite" 
   connectionString="REFERENCES" xmlns="http://santedb.org/bi">
  <meta version="1.0.0" status="active">
    <authors>
      <add>Sample Organization</add>
    </authors>
    <annotation>
      <div xmlns="http://www.w3.org/1999/xhtml">
        <p>Reference data</p>
      </div>
    </annotation>
    <policies>
      <demand>1.3.6.1.4.1.33349.3.1.5.9.2.0.11</demand>
    </policies>
  </meta>
</BiDataSourceDefinition>
```

The example above includes metadata, this is used for user interfaces as well as report building infrastructure in SanteDB. It is also possible to block access to a data source based on one or more policies which the user executing any report must have.

### Parameter Definitions

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

### Query Definitions

The BI infrastructure definition of queries allow multiple invariant representations of a query. For example, one query definition may define SQL for Firebird, PostgreSQL and SQLite . The runtime environment will determine which invariant SQL query to run. For example, if we wanted to reference data for PostgreSQL and Firebird as org.custom.query.ageWeight

```markup
<BiQueryDefinition xmlns="http://santedb.org/bi" id="org.santedb.bi.core.query.session" label="ui.santedb.bi.core.query.session">
  <meta status="active">
    <authors>
      <add>Sample Organization</add>
    </authors>
    <annotation>
      <div xmlns="http://www.w3.org/1999/xhtml">
        <p>Age ranges with healthy weights</p>
      </div>
    </annotation>
  </meta>
  <dataSources>
    <add ref="#org.custom.dataSource.references"/>
  </dataSources>
  <parameters>
    <add ref="#org.custom.parameter.version" name="version-name" type="string" required="false"/>
  </parameters>
  <definitions>
    <add>
      <providers>
        <invariant>npgsql</invariant>
      </providers>
      <![CDATA[
        select
          min_age, 
          max_age, 
          zneg1,
          z,
          zpos1
        from 
	        ref_weights
        where
          version = ${version-name}
      ]]>
    </add>
    <add>
      <providers>
        <invariant>fbsql</invariant>
      </providers>
      <![CDATA[
        select
          m_age as min_age, 
          x_age as max_age, 
          zn1 as zneg1,
          z,
          zp1 as zpos1
        from 
	        ref_weights
        where
          version = ${version-name}
      ]]>
    </add>
  </definitions>
</BiQueryDefinition>
```

