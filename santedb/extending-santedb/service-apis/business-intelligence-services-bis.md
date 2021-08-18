# Business Intelligence Service \(BIS\)

The Business Intelligence Service \(BIS\) provides a REST based wrapper around the [SanteDB BI Services infrastructure](../applets/business-intelligence-bi-assets/).  This interface allows your applications to interact with the underlying BI query infrastructure.

## Response Formats

The BIS supports responses in the following formats:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Format</th>
      <th style="text-align:left">Content-Type</th>
      <th style="text-align:left">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">HTML</td>
      <td style="text-align:left">text/html</td>
      <td style="text-align:left">
        <p>On the report rendering resource HTML response is triggered</p>
        <p>by affixing <code>htm</code> or <code>html</code> to the report path. For
          example:</p>
        <p><code>GET /bis/Report/html/test.report</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CSV</td>
      <td style="text-align:left">text/csv</td>
      <td style="text-align:left">
        <p>On the report rendering resource,. CSV is triggered by affixing <code>csv</code>
        </p>
        <p>to the report path, for example:</p>
        <p><code>GET /bis/Report/csv/test.report</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">XLS</td>
      <td style="text-align:left">application/
        <br />vnd.ms-excel</td>
      <td style="text-align:left">
        <p>On the report report rendering resource, XLS is triggered by affixing <code>xls</code>
        </p>
        <p>to the report path, for example:</p>
        <p><code>GET /bis/Report/xls/rest.report</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">JSON</td>
      <td style="text-align:left">application/json</td>
      <td style="text-align:left">All resources on the BIS support rendering via JSON</td>
    </tr>
    <tr>
      <td style="text-align:left">XML</td>
      <td style="text-align:left">application/xml</td>
      <td style="text-align:left">All resources on the BIS support rendering via XML</td>
    </tr>
  </tbody>
</table>



