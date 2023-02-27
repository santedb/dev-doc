# Configuration Tool

The SanteDB configuration tool is a graphical tool which is used to control the [SanteDB Configuration](../host-configuration-file/) file.

## Initial Configuration

Whenever you install SanteDB in a new environment you will be prompted to run the Configuration Tool. On initial configuration the configuration tool will show its initial configuration screen.

![Initial Configuration](<../../../.gitbook/assets/image (418) (1) (1) (1) (1) (1) (1) (1).png>)

The options are:

* **Easy Configuration** -> Sets a series of defaults from the selected **Template**
* **Advanced Configuration** -> Creates an empty configuration file which administrators can use individual configuration panels to control the overall configuration.

In most cases the Easy Configuration should be used.

### Database Configuration

When using the easy configuration option, the tool will allow you to set a database connection which you'd like to connect to.&#x20;

For more information on database connections see the [Database Connections](persistence-settings/database-connections.md) page.

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

![](<../../../.gitbook/assets/image (484).png>)

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

By default the simple editor is shown. The simple editor groups functions into logical feature sets and groups them in a manner which better illustrates what the feature is. There are occasions (for example, third party plugins) where a 1 to 1 representation of the configuration file is desired. This can be accessed via the **Setting Editor.**&#x20;

![](<../../../.gitbook/assets/image (417) (1) (1) (1).png>)

This view allows administrators to directly edit the configuration file - regardless if the feature has implemented the necessary [Configuration Panel Interfaces](../../../developers/extending-santesuite/extending-santedb/server-plugins/implementing-.net-features/configuration/configuration-panels.md).

### Applying Configuration

Editing the configuration values doesn't actually save the configuration file. When you change values in the configuration panel the tool calculates a list of changes that need to occur to apply the changes you've set. In order to apply these use the **Apply Changes** button on the command bar.

![](<../../../.gitbook/assets/image (463).png>)

Each feature that you've edited creates one or more tasks that will be executed. Each task can be investigated to gather details of the feature and what is being changed in your configuration file.

You can disable a feature step by clicking on the checkmark beside it. This instructs the configuration tool to not apply the task.&#x20;

{% hint style="warning" %}
Disabling a configuration task may result in the feature being partially enabled and not operating correctly.&#x20;
{% endhint %}

## Protected Configurations

Starting with SanteDB 3.0, configuration files can be partially encrypted using a certificate in the machine's store. When configuring SanteDB 3.0, you will be prompted if you wish to encrypt sensitive parts of the configuration file. This will encrypt:

* The connection strings to the SanteDB databases
* The Security Configuration including any HMAC secrets

When applying a configuration, the configuration tool will prompt the administrator if protection should be enabled:

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Selecting "yes" will prompt for the selection of a security certificate to protect the configuraiton file.

<figure><img src="../../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Ensure that the selected certificate is available to all application hosts which are using the configuration file.
{% endhint %}



For an example of the impact of protecting the configuration file, the data persistence configuration section in an unprotected configuration file will expose all connection details:

```xml
<section xsi:type="DataConfigurationSection">
    <connectionStrings>
      <add name="main" value="Data Source=testmpi_pwd.sqlite;Password=Test123" provider="sqlite" />
    </connectionStrings>
  </section>
```

However, in a protected configuration, the contents of this section are encrypted:

```xml
<section xsi:type="SanteDBProtectedConfigurationSectionWrapper" t="SanteDB.Core.Configuration.Data.DataConfigurationSection, SanteDB.Core.Api, Version=3.0.0.0, Culture=neutral, PublicKeyToken=null">
    <c>fhVkQ/wvv299hVNlQBtku9q7Cm2fR8GGk6MoiGqQ2l/xDtWN989oCsWcwJSRSji/8Uwp9Jubzx2yWRq6tdABSjWvopSx0SPN/O4+b3f9UUbuI/NPR1qzAKzFRfJU1Ox8YyACs6wWI7hfgC1M3VsGsyF3X2jzuxiu7CwFxk2U56vujj1OXl9gdA6WX9uc/87gFP7yC9oGmBcBCPl2KHHdE5WODeNutzjRXx+zJYqHPoNIadA/4wyVNKNY0VJ3wG6Lm5FybOmYkvID6g4J7euSCkmgHcOyyq44C2yHc86OjLdxvJP43hqv8id9zUKakomen9xGdj2I5GOgF0W80haQZE2u+7MqKfwC4rAm3aMXwRT4QbOZ9o+KcOCtPX091BHX/gmw+dXNgjkPIEUXL+CKXxZnD6B+VMAF9DQsSKOilN11JYJidn1p1rAJ6SG6ds1MJZzwzScwxsV+cnMXR1WTMVk42D2OaXiDhePnB5vFXIA=</c>
    <i>xL08UczD2pAZygPQ34CFdQ==</i>
  </section>
```
