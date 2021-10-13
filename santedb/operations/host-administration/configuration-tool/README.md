# Configuration Tool

The SanteDB configuration tool is a graphical tool which is used to control the [SanteDB Configuration](../host-configuration-file/) file.

## Initial Configuration

Whenever you install SanteDB in a new environment you will be prompted to run the Configuration Tool. On initial configuration the configuration tool will show its initial configuration screen.

![Initial Configuration](<../../../../.gitbook/assets/image (418) (1) (1).png>)

The options are:

* **Easy Configuration** -> Sets a series of defaults from the selected **Template**
* **Advanced Configuration **-> Creates an empty configuration file which administrators can use individual configuration panels to control the overall configuration.

In most cases the Easy Configuration should be used.

### Database Configuration

When using the easy configuration option, the tool will allow you to set a database connection which you'd like to connect to. 

For more information on database connections see the [Database Connections](database-connections.md) page.

### Instance Name

If you're running multiple copies of SanteDB on the same server environment, the named instance is the differentiation between these instances. The configuration tool will register the appropriate instance name service on your Windows operating system to start/stop the instance.

### Template

SanteDB iCDR servers have hundreds of configuration options. The `Template` option allows you to quickly select a configuration template which has pre-configured values as a starter for your configuration. The templates which are commonly used are:

* SanteDB MDM -> Configuration with Master Data Management enabled
* SanteMPI Server -> Configuration with the SanteMPI interfaces pre-configured
* SanteGuard Server -> Configuration with the SanteGuard interfaces pre-configured.

If you do not select a template, you will need to configure each plugin in the server.

## Using the Tool

When you have completed initial configuration you will be presented with a user interface as shown.

![](<../../../../.gitbook/assets/image (425) (1) (1).png>)

1. Feature List -> Shows a list of all features enabled in the SanteDB iCDR server which can be configured. (based on installed options)
2. Feature Configuration -> The configuration options for the selected feature.
3. Command Bar -> Used to open a backup configuration, apply changes or restart the Windows Service
4. Diagnostics Area -> Shows any errors or warnings that occur during setup / configuration.
5. Advanced Editor -> Opens the advanced editor for the configuration tool.

### Enabling or Disabling a Feature

The feature list shows one of three icons based on the current state of the feature in your SanteDB iCDR server:

* Enabled (Checkmark) -> All services and configuration sections required for the feature to operate are enabled.
* Disabled (Cross) -> No service or configuration section for the feature is enabled.
* Partially Enabled -> Some of the services and configuration values are present but the feature may not operate or may operate in a degraded state.

To enable or disable a feature, use the ENABLE or DISABLE link on the feature configuration panel.

### Advanced Editor

By default the simple editor is shown. The simple editor groups functions into logical feature sets and groups them in a manner which better illustrates what the feature is. There are occasions (for example, third party plugins) where a 1 to 1 representation of the configuration file is desired. This can be accessed via the **Setting Editor. **

![](<../../../../.gitbook/assets/image (417) (1).png>)

This view allows administrators to directly edit the configuration file - regardless if the feature has implemented the necessary [Configuration Panel Interfaces](../../../extending-santedb/server-plugins/implementing-.net-features/configuration/configuration-panels.md).

### Applying Configuration

Editing the configuration values doesn't actually save the configuration file. When you change values in the configuration panel the tool calculates a list of changes that need to occur to apply the changes you've set. In order to apply these use the **Apply Changes** button on the command bar.

![](<../../../../.gitbook/assets/image (420) (1) (1).png>)

Each feature that you've edited creates one or more tasks that will be executed. Each task can be investigated to gather details of the feature and what is being changed in your configuration file.

You can disable a feature step by clicking on the checkmark beside it. This instructs the configuration tool to not apply the task. 

{% hint style="warning" %}
Disabling a configuration task may result in the feature being partially enabled and not operating correctly. 
{% endhint %}

