# SanteDB Schemas

When editing an asset in SanteDB which is in XML format, the use of an XML Schema can greatly assist the development process. The SanteDB community provides schemas for developers to use in their XML files at `http://santedb.org/schema/v3.0`or `http://santedb.org/schema/v2.2`.

## Schemas

| Schema Location            | Uses                                                                                                                                                                                                                                |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Applet.xsd`               | Applet Manifest (`manifest.xml`) - [#manifest-file](extending-santesuite/extending-santedb/applets/applet-structure.md#manifest-file "mention")                                                                                     |
| `Audit.xsd`                | HDSI format Audit messages                                                                                                                                                                                                          |
| `BusinessIntelligence.xsd` | Any BI asset: `BiIndicatorDefinition`, `BiQueryDefinition`, `BiViewDefinition`, `BiReportDefinition` - [business-intelligence-bi-assets](extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/ "mention") |
| `Cdss.xsd`                 | Clinical Decision Support rules expressed in XML - [cdss-definitions.md](applets/cdss-protocols/cdss-definitions.md "mention")                                                                                                      |
| `Dataset.xsd`              | Any dataset file (seeding data) [distributing-data.md](extending-santesuite/extending-santedb/applets/distributing-data.md "mention")                                                                                               |
| `DetectedIssue.xsd`        | HDSI format detected issue templates                                                                                                                                                                                                |
| `ForeignData.xsd`          | Any Foreign Data Map definition file ( [external-data-maps.md](applets/external-data-maps.md "mention"))                                                                                                                            |
| `MatcherDefinition.xsd`    | Any match configuration file - [matching-engine.md](../santedb/matching-engine.md "mention")                                                                                                                                        |
| `ModelMap.xsd`             | For .NET plugins where a persistence layer (physical layer) class definition must be mapped to a business layer object.                                                                                                             |
| `ViewModelDescription.xsd` | For defining view model definition files which control how the HDSI - [#viewmodel-json](service-apis/health-data-service-interface-hdsi.md#viewmodel-json "mention")                                                                |

## Referencing Schemas

To reference a schema in your XML file, simply:

* Declare the `http://www.w3.org/2001/XMLSchema-instance`namespace on your root element
* Use the `xsi:schemaLocation`attribute to point to the intended schema

For example, if defining BI Indicator:

```xml
<BiIndicatorDefinition 
    xmlns="http://santedb.org/bi"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://santedb.org/bi http://santedb.org/schema/v3.0/BusinessIntelligence.xsd"
    id="org.example.indicator"
    name="Example Indicator"
    label="ui.org.example.indicator.label">
</BiIndicatorDefinition>
```



