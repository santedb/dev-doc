# BI Asset Definitions

 BI assets are defined in the /bi folder of your applet and can contain:

* BiPackages - A collection of BI assets for a particular purpose (for example: a custom report including parameters and queries)
* BiDataSource - Defines a connection to a particular data source such as relational data or custom IBiDataProvider instance written in .NET.
* BiParameterDefinitions - Defines a reusable parameter for use in queries and reports. Parameter definitions define the type, validation, and data source (lists) for inputs into queries.
* BiQueryDefinition - Defines a common query against one or more data sources (example: master patient list)
* BiViewDefinition - Defines a view on top of a BiQueryDefinition. This allows for data source independent aggregation and pivoting of results.
* BiReportDefinition - Defines a user friendly view of data defined in a view.

All BI assets are defined in XML in the **http://santedb.org/bi **namespace. The schema for this namespace is in the Schema\ directory of your SanteDB installation.

### Uses of BI Assets

It is recommended to use BI assets for reports within your applet as these components are available via a multitude of interfaces. For example, defining a BI View for "Registered Patients by Gender" would expose this data via:

* The REST API as JSON - Meaning third party applications can consume the data directly
* User Interfaces as Report - Meaning the UI can use the same data to construct charts, tables, etc.
* FHIR Measure Report - Meaning that FHIR services can obtain the data from the view as  a measure report (In the roadmap)
