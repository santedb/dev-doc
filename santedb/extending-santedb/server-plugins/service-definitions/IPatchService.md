---
description: IPatchService (SanteDB.Core.Api)
---

## Summary
Represents a patch service which can calculate and apply patches

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


## Implementations


### Basic Patching Service - (SanteDB.Core.Api)
Represents a simple patch service which can calculate patches and apply them

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.SimplePatchService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPatchService : SanteDB.Core.Services.IPatchService { 
	public String ServiceName => "My own IPatchService service";
	/// <summary>
	/// Performs a DIFF and creates the related patch which can be used to update             to
	/// </summary>
	public SanteDB.Core.Model.Patch.Patch Diff(SanteDB.Core.Model.IdentifiedData existing,SanteDB.Core.Model.IdentifiedData updated,System.String[] ignoreProperties){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Apples the specified  onto  returning the updated object
	/// </summary>
	public SanteDB.Core.Model.IdentifiedData Patch(SanteDB.Core.Model.Patch.Patch patch,SanteDB.Core.Model.IdentifiedData data,System.Boolean force){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Tests that the patch can be applied on the specified object
	/// </summary>
	public System.Boolean Test(SanteDB.Core.Model.Patch.Patch patch,SanteDB.Core.Model.IdentifiedData target){
		throw new System.NotImplementedException();
	}
}
```
