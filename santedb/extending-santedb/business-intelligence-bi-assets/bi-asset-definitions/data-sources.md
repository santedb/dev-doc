# Data Sources

BI Data Sources represent the source for data where queries are executed. A data source can be a relational data store \(such as a data store used by SanteDB infrastructure\) or an external data source \(such as a website, API, or reference data sets\).

The pre-defined BI datasources in SanteDB are outlined below:

| ID | Service | Description |
| :--- | :--- | :--- |
| org.santedb.bi.dataSource.main | SanteDB | Primary transaction database for SanteDB or the DC |
| org.santedb.bi.dataSource.warehouse | SanteDB | The data warehouse connection containing pivoted data and ad-hoc data definitions. |
| org.santedb.bi.dataSource.audit | SanteDB | The primary audit database for the stock installation of SanteDB. |
| org.santedb.sg.bi.dataSource.audit | SanteGuard | The connection string for SanteGuard's enhanced audit repository. |

### Data Source Definition Files

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

