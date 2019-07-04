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



