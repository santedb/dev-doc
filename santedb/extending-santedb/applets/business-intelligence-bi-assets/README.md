# Business Intelligence Assets

SanteDB supports the generation of reports and fetching of aggregate data for charting and business intelligence functions \(such as FHIR MeasureReport resources\)  using the BI infrastructure.

This series of functions allows reporting values generated by SanteDB to be consistent whether they are fetched from FHIR, in the user interface, or REST API. You would use the BI services when:

* You want to expose a calculated measure to consumers \(counts, sums, etc.\)
* You want to render charts, tables, or free-form views from the SanteDB database
* You need to pivot/aggregate and analyze data in some manner
* You have to integrate with a third party HMIS system using FHIR, SDMX-HD or other mechanism.
* You want a rapid way to expose discrete data over the BI API to a third party system which does not need the full power of the SanteDB query engine.

### Recommended Tooling

* SanteDB Software Development Kit
* Database Management Software - We recommend DBeaver Community Edition as it can connect to SQlite, PostgreSQL and Firebird from one tool.
* XML Editor - We recommend Visual Studio Community, however any XML editor will do. One that is able to read XSD and provide auto-complete will provide the best experience.
