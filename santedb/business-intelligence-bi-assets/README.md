# Business Intelligence Services

SanteDB supports the generation of reports and fetching of aggregate data for charting and business intelligence functions \(such as FHIR MeasureReport resources\)  using the BI infrastructure. BI assets are defined in the /bi folder of your applet and can contain:

* BiPackages - A collection of BI assets for a particular purpose \(for example: a custom report including parameters and queries\)
* BiDataSource - Defines a connection to a particular data source such as relational data or custom IBiDataProvider instance written in .NET.
* BiParameterDefinitions - Defines a reusable parameter for use in queries and reports. Parameter definitions define the type, validation, and data source \(lists\) for inputs into queries.
* BiQueryDefinition - Defines a common query against one or more data sources \(example: master patient list\)
* BiViewDefinition - Defines a view on top of a BiQueryDefinition. This allows for data source independent aggregation and pivoting of results.
* BiReportDefinition - Defines a user friendly view of data defined in a view.

All BI assets are defined in XML in the **http://santedb.org/bi** namespace. The schema for this namespace is in the Schema\ directory of your SanteDB installation.

### 

