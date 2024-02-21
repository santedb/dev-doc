# Data Quality Rules

{% hint style="info" %}
This page documents a feature which is only available in SanteDB 3.0
{% endhint %}

SanteDB allows system administrators to manage the data quality rules from the administration panel. Data quality rules are applied to all objects which are configured and result in a detected issue extension being added to the persisted object. This information can then be viewed (for example: [Data Quality Tab in SanteMPI](../../../../user-guides-and-training/santempi/the-patient-dashboard/data-quality-tab.md)) used in matching configurations to prevent matching of records with data quality problems, or called when the `$validate` method is invoked on the HDSI.

<figure><img src="../../../../.gitbook/assets/image (521).png" alt=""><figcaption></figcaption></figure>

## Editing Data Quality Rules

### Core Properties

Editing data quality rules and creating a new set of data quality rules is a very similar process. First, the data quality properties are populated:&#x20;

<figure><img src="../../../../.gitbook/assets/image (522).png" alt=""><figcaption></figcaption></figure>

* **Identifier:** The unique data quality rule identiifer for the entire rule configuration. This must be unique to the SanteDB deployment.
* **Name:** The name of the data quality rules configuration, this is a human readable name referenced by administrators in log files and on the UI.
* **Active:** When selected, indicates that the rules should be applied to all inbound objects.

### Resources

Each rule configuration contains one or more resource types that the rules apply to. When adding a new resource type, the administrator must select the type of resource to which the rule applies. Then one or more assertions are added to the resource. For example, to create a data quality rule for weights which are negative.

<figure><img src="../../../../.gitbook/assets/image (523).png" alt=""><figcaption></figcaption></figure>
