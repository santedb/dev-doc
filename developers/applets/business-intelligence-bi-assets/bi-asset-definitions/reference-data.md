# Reference Data

{% hint style="info" %}
This page documents a feature in SanteDB 3.0
{% endhint %}

Reference data sets are a specialized `<dataSource>` which may be placed into a report, or defined on their own which contain static comma-separated-values (CSV) of data which is to be referenced. Reference data acts the same way that regular SQL [queries.md](../../../extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/bi-asset-definitions/queries.md "mention") or [views.md](../../../extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/bi-asset-definitions/views.md "mention") work.

```xml
<BiReferenceDataSourceDefinition xmlns="http://santedb.org/bi" 
    name="friendly name"
    id="dotted.id.of.refset">
    <![CDATA[Column1, Column2, Column3,
    R1_C1, R1_C2, R1_C3
    R2_C1, R2_C2, R2_C3
    ]]>
</BiReferenceDataSourceDefinition>
```
