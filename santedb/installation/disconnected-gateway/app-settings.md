# App Settings

When installing SanteDB dCDR you may be asked to provide additional settings for the application. These settings are used to control the behavior of the dCDR.

| Setting | Value | Description |
| :--- | :--- | :--- |
| http.bindAddress | 0.0.0.0:9200 | The IP / Port to bind the dCG user interfaces to. |
| aa.preferred | MOH\_NHID | The most preferred assigning authority / identity domain to show on the user interface. |
| security.localUsers | true \| false | True if local security accounts should be permitted |
| input.name | simple \| structured | Simple = Names are entered as text boxes , Structured = Names are tokenized |
| input.address | text \| structured \| select | Text = Address components are free-text inputs, Structured = Address components for State / County are drop-downs and street address is input text , Select = Address is selected from pre-determined list of addresses. |
| forbid.patient.name.family | true \| false | When true, do not collect family names |
| forbid.patient.name.prefix | true \| false | When true, do not collect prefix information |
| forbid.patient.name.suffix | true \| false | When true, do not collect suffix information |
| forbit.patient.name.given | true \| false | When true, do not collect given names |

