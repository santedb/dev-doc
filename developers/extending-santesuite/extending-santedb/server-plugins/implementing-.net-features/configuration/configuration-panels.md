# Configuration Panels

Whenever your .NET plugin exposes functionality to the iCDR service instance, and requires custom configuration sections, it is best practice to expose functions to allow administrators to configure your plugin on the iCDR server.&#x20;

## Features

Features are located on the left hand side of the configuration tool, as shown below:

![](<../../../../../../.gitbook/assets/image (398).png>)

Each of these features is discovered by scanning your .NET assembly for implementations of `IFeature` , an `IFeature` defines the following properties:

* Group -> The logical grouping where the feature should reside
* Description -> A textual description of the feature which is to appear on the detailed configuration
* ConfigurationType -> The type of object that the feature is expecting to appear in the configuration file
* Name -> The name of the feature to appear in the feature list

The `IFeature` expects implementers to provide a function called `QueryState` , this method should scan the provided configuration instance and return on of the following values based on the status of the feature in the provided configuration:

* `NotInstalled` The feature could not be detected in the provided configuration instance
* `PartiallyInstalled` The feature has some attributes on the configuration file, but is incomplete for full feature startup
* `Installed` The feature is enabled

When a feature is enabled the `CreateInstallTasks` method is called, and should return one or more `IConfigurationTask` instances which perform the setup/enable function. Conversely, when the feature is disabled, the `CreateUninstallTasks` method is called.

### Configuration Tasks

The `IConfigurationTask` interface is used to control individual configuration steps to modify the provided file to perform a configuration or removal of a feature. You can see these in the confirm tasks dialog.\


![](<../../../../../../.gitbook/assets/image (400).png>)

Each task can be enabled/disabled by an administrator to skip the specified task in their environment.

When the administrator clicks `Ok` on the `Confirm Tasks` dialog box, the `IConfigurationTask` method `VerfiyState` is called. Your task should verify that the task is required, or should run, if so the `VerifyState` method should return true.&#x20;

The `Execute` method of the task should perform the necessary configuration tasks to alter the configuration for the administrator. The `Rollback` method is called in the case of an error in applying the configuration changes.&#x20;

{% hint style="danger" %}
Do not save the configuration passed to the Execute or Rollback methods. The saving of the configuration is handled by the configuration tooling. Your methods should only update the configuration variable passed to the method call.
{% endhint %}

## Annotating Service Classes

The configuration tooling in SanteDB uses the .NET `PropertyGrid` control to expose configuration options. It is recommended that you use the attributes listed below on your properties to allow for proper user experience for configuration of your plugin.

| Attribute         | Use                                                                                           | Example                                              |
| ----------------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| `[DisplayName]`   | Controls the display name of the configuration property                                       | `[DisplayName("Server URL")]`                        |
| `[Description]`   | Provides contextual help on the property grid which describes how the setting should be used. | `[Description("The remote endpoint of the server")]` |
| `[Browsable]`     | Use this attribute to control whether your setting should appear in the configuration tool.   | `[Browsable(false)]`                                 |
| `[ReadOnly]`      | When your configuration setting needs to be shown, but not edited.                            | `[ReadOnly(true)]`                                   |
| `[Editor]`        | When you would like to allow a user to edit the value using a complex editor (see below)      |                                                      |
| `[TypeConverter]` | The type converter used to convert input from the property grid to/from the class.            |                                                      |

{% hint style="info" %}
For more information on how to use the PropertyGrid settings see [https://www.codeproject.com/articles/22717/using-propertygrid](https://www.codeproject.com/articles/22717/using-propertygrid)
{% endhint %}

### Custom Editors

You can instruct the property grid to use a custom editor for your values. In addition to the standard .NET editors, SanteDB provides additional editors.

#### Resource Selector

When you wish to expose restrictions on resource types for your plugin, you would normally use a collection of `ResourceTypeReferenceConfiguration` .

```csharp
[XmlElement("resources"), JsonProperty("resources")]
[DisplayName("Allowed Resources"), Description("Set the resources allowed")]
public List<ResourceTypeReferenceConfiguration> Resources { get; set; }
```

You can allow users to select defined resources in this property value by using referencing the resource selector editor with:

```csharp
[XmlElement("resources"), JsonProperty("resources")]
[DisplayName("Allowed Resources"), Description("Set the resources allowed")]
[Editor("SanteDB.Configuration.Editors.ResourceCollectionEditor, SanteDB.Configuration", 
  "System.Drawing.Design.UITypeEditor, System.Drawing, Version=4.0.0.0")]
public List<ResourceTypeReferenceConfiguration> Resources { get; set; }
```

#### Type Editor

You can allow users to select from any system type which you'd like referenced on your solution whenever a `TypeReferenceConfiguation` property is needed. For example, if your plugin has configuration for more functions as:

```csharp
[XmlElement("plugins"), JsonProperty("plugins")]
[DisplayName("Enabled Plugins"), Description("Extended Plugins You want to use")]
public List<TypeReferenceConfiguration> Extensions { get; set; }
```

You can annotate the class with the type editor:

```csharp
[Editor("SanteDB.Configuration.Editors.TypeSelectorEditor, SanteDB.Configuration", 
     "System.Drawing.Design.UITypeEditor, System.Drawing"), Binding(typeof(IFhirResourceHandler))]
[XmlElement("plugins"), JsonProperty("plugins")]
[DisplayName("Enabled Plugins"), Description("Extended Plugins You want to use")]
public List<TypeReferenceConfiguration> Extensions { get; set; }
```

Additionally, using the `Binding` attribute will allow you to filter from any type to a specific type. For example, to only allow selection of a type which implements `IMyPluginExtension`:

```csharp
[Editor("SanteDB.Configuration.Editors.TypeSelectorEditor, SanteDB.Configuration", 
     "System.Drawing.Design.UITypeEditor, System.Drawing"), Binding(typeof(IFhirResourceHandler))]
[Binding(typeof(IMyPluginExtension))]
[XmlElement("plugins"), JsonProperty("plugins")]
[DisplayName("Enabled Plugins"), Description("Extended Plugins You want to use")]
public List<TypeReferenceConfiguration> Extensions { get; set; }
```

