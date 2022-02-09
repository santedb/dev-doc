# General Properties

The general properties tab of the match configuration is used to control the general settings of the match configuration. When creating a new match configuration, the panel will default to edit mode to allow for capture of the properties.

![](<../../../.gitbook/assets/image (441).png>)

The fields on this properties panel are:

* **ID**: A unique identifier for the match configuration. This identifier is used in configurations, logs, and in the SanteDB API to control configuration settings used for specific match use cases. this field must not contain spaces, or special characters beyond periods or hyphens.
* **Resources:** The resources input allows the administrator to select the type of resource to which the match configuration applies. This is used by callers of the matching engine to collect candidate match configurations which could be used to classify / score the data.
* **Tags:** Tags provide implementation specific (or plugin specific) controls for the match configuration. These can vary depending on the use of the match configuration (i.e. in MDM, import, etc.)
* **Description:** Provides a human readable description of the configuration.

## Tags

By default, only the MDM layer in the SanteDB iCDR will use the tags setting.&#x20;

| Tag              | Type    | Description                                                                                                                                                                 |
| ---------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$mdm.auto-link` | Boolean | When true, instructs the MDM layer to automatically link records together when the `$input` and `$block` records are classified as a match. Otherwise, matches are flagged. |

###
