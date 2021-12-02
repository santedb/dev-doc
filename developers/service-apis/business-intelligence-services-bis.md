# Business Intelligence Service (BIS)

The Business Intelligence Service (BIS) provides a REST based wrapper around the [SanteDB BI Services infrastructure](../applets/business-intelligence-bi-assets/).  This interface allows your applications to interact with the underlying BI query infrastructure.

## Response Formats

The BIS supports responses in the following formats:

| Format | Content-Type                        | Notes                                                                                                                                                                                                           |
| ------ | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTML   | text/html                           | <p>On the report rendering resource HTML response is triggered</p><p>by affixing <code>htm</code> or <code>html</code> to the report path. For example:</p><p><code>GET /bis/Report/html/test.report</code></p> |
| CSV    | text/csv                            | <p>On the report rendering resource,. CSV is triggered by affixing <code>csv</code></p><p>to the report path, for example: </p><p><code>GET /bis/Report/csv/test.report</code></p>                              |
| XLS    | <p>application/<br>vnd.ms-excel</p> | <p>On the report report rendering resource, XLS is triggered by affixing <code>xls</code></p><p>to the report path, for example:</p><p><code>GET /bis/Report/xls/rest.report</code></p>                         |
| JSON   | application/json                    | All resources on the BIS support rendering via JSON                                                                                                                                                             |
| XML    | application/xml                     | All resources on the BIS support rendering via XML                                                                                                                                                              |

