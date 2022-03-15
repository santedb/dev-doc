# User Interface App Settings

When installing SanteDB dCDR you may be asked to provide additional settings for the application. These settings are used to control the behavior of the dCDR.

{% hint style="info" %}
You can edit these settings by opening the dCDR Configuration Files and editing the `<appSettings>` element.
{% endhint %}

| Setting                           | Value                        | Description                                                                                                                                                                                                              |
| --------------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| http.bindAddress                  | 0.0.0.0:9200                 | The IP / Port to bind the dCG user interfaces to.                                                                                                                                                                        |
| aa.preferred                      | MOH\_NHID                    | The most preferred assigning authority / identity domain to show on the user interface.                                                                                                                                  |
| security.localUsers               | true \| false                | True if local security accounts should be permitted                                                                                                                                                                      |
| input.name                        | simple \| structured         | Simple = Names are entered as text boxes , Structured = Names are tokenized                                                                                                                                              |
| input.address                     | text \| structured \| select | Text = Address components are free-text inputs, Structured = Address components for State / County are drop-downs and street address is input text , Select = Address is selected from pre-determined list of addresses. |
| forbid.patient.name.family        | true \| false                | When true, do not collect family names                                                                                                                                                                                   |
| forbid.patient.name.prefix        | true \| false                | When true, do not collect prefix information                                                                                                                                                                             |
| forbid.patient.name.suffix        | true \| false                | When true, do not collect suffix information                                                                                                                                                                             |
| forbit.patient.name.given         | true \| false                | When true, do not collect given names                                                                                                                                                                                    |
| forbid.patient.address.state      | true \| false                | When true, do not collect state in address forms                                                                                                                                                                         |
| forbid.patient.address.county     | true \| false                | When true, do not collect district or county information.                                                                                                                                                                |
| forbid.patient.address.city       | true \| false                | When true, do not collect city information.                                                                                                                                                                              |
| forbid.patient.address.precinct   | true \| false                | When true, do not collect precinct information                                                                                                                                                                           |
| forbid.patient.address.street     | true \| false                | When true, do not collect street information.                                                                                                                                                                            |
| forbid.patient.address.postalcode | true \| false                | When true, do not collect postal codes                                                                                                                                                                                   |
| optional.patient.name.given       | true \| false                | When true, collecting the patient given name is optional where it would otherwise be required.                                                                                                                           |
| optional.patient.name.family      | true \| false                | When true, collecting the patient family name is optional where it would otherwise be required.                                                                                                                          |
| optional.patient.address.state    | true \| false                | When true, collecting the patient is optional where it would otherwise be required.                                                                                                                                      |
| optional.patient.address.county   | true \| false                | When true, collecting the patient county is optional where it would otherwise be required.                                                                                                                               |
| optional.patient.address.city     | true \| false                | When true, collecting the patient city is optional where it would otherwise be required.                                                                                                                                 |
| allow.patient.religion            | true \| false                | When true, show inputs for capturing and displaying the patient religion field.                                                                                                                                          |
| allow.patient.ethnicity           | true \| false                | When true, show inputs for capturing and displaying patient ethnicity field.                                                                                                                                             |