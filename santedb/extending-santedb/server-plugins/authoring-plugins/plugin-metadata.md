# Plugin Metadata

Plugin management is performed via a series of assembly attributes which are embedded in the assembly manifest of the iCDR plugins. The following attributes are to be used for identifying plugin metadata:

| **Attribute** | **Use** | **Description** |
| :--- | :--- | :--- |
| AssemblyVersion | R | Identifies the version \(major.minor.revision.build\) of the plugin. This information is used for dependency information. |
| AssemblyInformationalVersion | O | An informational version which is displayed on the administration and management service interface. |
| AssemblyDescription | R | A human readable description of the plugin to appear on the administrative interface. |
| AssemblyCopyright | O | Copyright information and/or use restriction messages. |
| Plugin | R | Identifies the assembly as a plugin. The plugin attribute identifies the minimum version of the SanteDB core which is required to run the plugin. |
| PluginDependency | O | Identifies the name and version of a dependency upon which the plugin must have installed. |

{% hint style="info" %}
The AssemblyVersion, AssemblyInformationalVersion, AssemblyDescription and AssemblyCopyright attributes are automatically generated for .NET Standard projects, therefore if your plugin is targeting the shared infrastructure, you do not need to manually edit these attributes. For .NET Framework 4.7 projects, these attributes can be found in the Properties\AssemblyInfo.cs file.
{% endhint %}

