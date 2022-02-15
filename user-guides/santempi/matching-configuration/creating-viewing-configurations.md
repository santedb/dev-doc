# Creating / Viewing Configurations

When editing or creating a match configuration, users will be presented with the match configuration detail screen.

![](<../../../.gitbook/assets/image (430) (1) (1).png>)

When creating a new configuration, the sections of the configuration are shown based on the current required information contained within the configuration. For example, the scoring section tab will not appear until after the blocking configuration has been entered and saved.

By default, the act of creating a new configuration will result in the contained panels defaulting to edit mode.

## Configuration State

Matching configurations can be in one of two states:

* Active - The configuration should be used by the MDM layer to detect and flag duplicates and (if configured) perform merging of those records.
* Inactive - The configuration is not being used by the MDM or registration layer to detect duplicates. This is the default state of a new match configuration.

When editing or modifying a match configuration, the recommended process is:

1. Disable the configuration if it is currently active
2. Make the necessary changes to the configuration
3. Test the changes to the configuration
4. Activate the configuration

{% hint style="info" %}
In a production system, it is recommended that users clone a match configuration and edit the clone of the configuration - such that the old configuration can be restored easily.
{% endhint %}

## HTML Export

When a user needs to share a match configuration with others (such as those using another software package) or requires unchangeable description of the match configuration (for their implementation documentation, for example) an HTML export of the configuration file can be obtained using the `HTML` button. This produces a report which details the configuration and allows for printing of the logic and settings used.

![](<../../../.gitbook/assets/image (445) (1) (1).png>)

## Configuration Sections

{% content-ref url="general-properties.md" %}
[general-properties.md](general-properties.md)
{% endcontent-ref %}

{% content-ref url="blocking-configuration.md" %}
[blocking-configuration.md](blocking-configuration.md)
{% endcontent-ref %}

{% content-ref url="scoring-configuration.md" %}
[scoring-configuration.md](scoring-configuration.md)
{% endcontent-ref %}

{% content-ref url="classification-configuration.md" %}
[classification-configuration.md](classification-configuration.md)
{% endcontent-ref %}

{% content-ref url="testing-configurations.md" %}
[testing-configurations.md](testing-configurations.md)
{% endcontent-ref %}
