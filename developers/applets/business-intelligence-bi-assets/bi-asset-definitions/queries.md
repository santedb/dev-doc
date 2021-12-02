# Queries

Queries in the SanteDB BI services infrastructure allow the definition of a single identified query which can be referenced by reports or views. Queries abstract the underlying query mechanic of the RDBMS and present a logical view of data fed from that data source.

Queries should:

1. Always return consistent column names between invariant SQL definitions.
2. Be reusable where possible, representing a logical construct (patients, providers, sessions, etc.)
3. Define at least npgsql and sqlite definitions

Queries loosely translate to fact sources.

### Query Definition Files

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

{% hint style="info" %}
Queries can pull data from multiple data sources, however this function is only supported if the underlying data source provider supports attaching additional data sources (for example: SQLite)
{% endhint %}
