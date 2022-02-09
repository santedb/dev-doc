# General Configuration

The general configuration tab shows metadata related to the configuration as well as an overall explanation of the configuration's matching process.

## Properties Panel

The general properties tab of the match configuration is used to control the general settings of the match configuration. When creating a new match configuration, the panel will default to edit mode to allow for capture of the properties.

![](<../../../.gitbook/assets/image (441) (1).png>)

The fields on this properties panel are:

* **ID**: A unique identifier for the match configuration. This identifier is used in configurations, logs, and in the SanteDB API to control configuration settings used for specific match use cases. this field must not contain spaces, or special characters beyond periods or hyphens.
* **Resources:** The resources input allows the administrator to select the type of resource to which the match configuration applies. This is used by callers of the matching engine to collect candidate match configurations which could be used to classify / score the data.
* **Tags:** Tags provide implementation specific (or plugin specific) controls for the match configuration. These can vary depending on the use of the match configuration (i.e. in MDM, import, etc.)
* **Description:** Provides a human readable description of the configuration.

### Tags

By default, only the MDM layer in the SanteDB iCDR will use the tags setting.&#x20;

| Tag              | Type    | Description                                                                                                                                                                 |
| ---------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$mdm.auto-link` | Boolean | When true, instructs the MDM layer to automatically link records together when the `$input` and `$block` records are classified as a match. Otherwise, matches are flagged. |

## Explain Diagram

The explain diagram for a configuration illustrates the overall matching process which will be undertaken for the overall matching process.&#x20;

![](<../../../.gitbook/assets/image (450).png>)

The explain diagram shows:

* The source resource type which will be read from the database
* The blocking instructions (or blocking filter instructions) which will be used to filter the source resource from the database.
* The scoring instructions and attributes to be used
* The classification thresholds for the classification stage.

## Related Topics

{% content-ref url="blocking-configuration.md" %}
[blocking-configuration.md](blocking-configuration.md)
{% endcontent-ref %}

{% content-ref url="scoring-configuration.md" %}
[scoring-configuration.md](scoring-configuration.md)
{% endcontent-ref %}

{% content-ref url="classification-configuration.md" %}
[classification-configuration.md](classification-configuration.md)
{% endcontent-ref %}
