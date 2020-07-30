---
description: >-
  This section describes the necessary steps and procedures to author your own
  C#/.NET based plugins
---

# Authoring Plugins

When authoring a plugin, it is important to understand the function of the plugin and how it will/should be used in the SanteDB host process.

## Plugin Libraries

All SanteDB components \(the iCDR, dCDR, and UI\) all leverage common packages. These packages are shared among a variety of the infrastructure components. 

![Library Relationship](../../../.gitbook/assets/image%20%2886%29.png)

When implementing your plugin, if, for example, you target .NET Framework and use the SanteDB.Server.Plugin package, then your plugin will not work on the dCDR. Conversely if you only reference APIs in the SanteDB Core Libs package then your plugin will work on all platforms SanteDB supports.

The general rule is:

* If you're creating a global .NET plugin select .NET Standard 2.0 as the project type
* If you're creating a SanteDB dCDR based plugin use either .NET Standard 2.0 or .NET Framework 4.7 
* If you're creating a SanteDB iCDR based plugin use .NET Framework 4.7

## Adding Nuget Dependencies

Once you've decided where your plugin fits into the SanteDB ecosystem you'll have to add your Nuget dependencies. All SanteDB Nuget packages are registered on the central Nuget repository, the table below identifies which SanteDB Nuget packages provide which functionality.

### 

