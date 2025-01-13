# BI Asset Definitions

&#x20;BI assets are defined in the /bi folder of your applet and can contain:

* BiPackages - A collection of BI assets for a particular purpose (for example: a custom report including parameters and queries)
* BiDataSource - Defines a connection to a particular data source such as relational data or custom IBiDataProvider instance written in .NET.
* BiParameterDefinitions - Defines a reusable parameter for use in queries and reports. Parameter definitions define the type, validation, and data source (lists) for inputs into queries.
* BiQueryDefinition - Defines a common query against one or more data sources (example: master patient list)
* BiViewDefinition - Defines a view on top of a BiQueryDefinition. This allows for data source independent aggregation and pivoting of results.
* BiReportDefinition - Defines a user friendly view of data defined in a view.

All BI assets are defined in XML in the **http://santedb.org/bi** namespace. The schema for this namespace is in the Schema\ directory of your SanteDB installation.

## Uses of BI Assets

It is recommended to use BI assets for reports within your applet as these components are available via a multitude of interfaces. For example, defining a BI View for "Registered Patients by Gender" would expose this data via:

* The REST API as JSON - Meaning third party applications can consume the data directly
* User Interfaces as Report - Meaning the UI can use the same data to construct charts, tables, etc.
* FHIR Measure Report - Meaning that FHIR services can obtain the data from the view as  a measure report (In the roadmap)

## Editing BI Assets

Editing BI assets is greatly assisted with the use of the SanteDB schemas. BI Assets are available from the SanteDB community server and can be referenced in your favorite XML editor with:

```xml
<BiViewDefinition xmlns="http://santedb.org/bi" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://santedb.org/bi http://santedb.org/schema/v3.0/BusinessIntelligence.xsd"
>
</BiViewDefinition>
```

This will enable auto completion and validation on your instance

<figure><img src="../../../../../../.gitbook/assets/image (542).png" alt=""><figcaption></figcaption></figure>

## Topics

{% content-ref url="data-sources.md" %}
[data-sources.md](data-sources.md)
{% endcontent-ref %}

{% content-ref url="parameters.md" %}
[parameters.md](parameters.md)
{% endcontent-ref %}

{% content-ref url="queries.md" %}
[queries.md](queries.md)
{% endcontent-ref %}

{% content-ref url="reports.md" %}
[reports.md](reports.md)
{% endcontent-ref %}
