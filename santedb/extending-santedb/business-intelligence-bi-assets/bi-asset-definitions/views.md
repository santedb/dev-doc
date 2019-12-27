# Views

BI Views are logical representations of data obtained from underlying queries. Where queries represent particular facts within a data source, views represent answers to particular questions. For example, you may have a query definition for "Patients", however a view for "Patients By Gender By Age". 

Views allow you to:

1. Aggregate data from queries using a common database independent syntax 
2. Pivot data from queries using defined buckets / columns
3. Further filter queries based on a sub-set of data

### View Definition Files

View definition files are defined using the BiViewDeifnition root.

```markup
<?xml version="1.0"?>
<BiViewDefinition xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" name="by-type-date" id="org.santedb.bi.core.view.session.type" xmlns="http://santedb.org/bi">
  <meta status="active">
    <authors>
      <add>SanteSuite Contributors</add>
    </authors>
  </meta>
  <query ref="#org.santedb.bi.core.query.session" />
  <aggregations>
    <add>
      <providers>
        <invariant>psql</invariant>
      </providers>
      <grouping>
        <column name="crt_utc">cast(crt_utc as DATE)</column>
        <column name="ses_typ">ses_typ</column>
      </grouping>
      <select>
        <column name="ses_typ" fn="value">ses_typ</column>
        <column name="ses_date" fn="value">cast(crt_utc as DATE)</column>
        <column name="n_sessions" fn="count-distinct">ses_id</column>
      </select>
    </add>
  </aggregations>
  <pivot key="ses_date" columnDef="ses_typ" value="n_sessions" fn="sum" />
</BiViewDefinition>
```



