# Data Marts

{% hint style="info" %}
This page documents a feature in SanteDB version 3.0.
{% endhint %}

## Introduction

SanteDB's Business Intelligence services allow developers of SanteDB applets to define custom reports, queries, views and also (starting with Version 3.0) custom data marts.&#x20;

A data mart is replica of the primary SanteDB database whereby selective data is pre-pivoted, calculated and stored in a schema which is more suited for running reports. This makes writing reports easier and makes running reports faster. It also allows system administrators to host data for reporting purposes on another physical server instance.

The SanteDB BI data mart infrastructure allows for the extension and derivation of datamarts on one another. A data mart definition is defined in a new bi asset file with a `DatamartDefinition` element and contains:

* Metadata about the data mart definition including authors, and permissions to access the data mart.
* A data source registration which identifies the `<dataSource` which can be referenced by reports, queries and views.
* A `<schema>` which identifies the tables, views and relationships between these objects within the datamart.
* A `<flows>` element which defines one or more data flows and data pipelines for extracting data from one or SanteDB data sources (including other data marts) to populate the new data mart.
