---
description: IBiRenderService (SanteDB.BI)
---

## Summary
BI Render service

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


## Implementations


### LocalBiRenderService - (SanteDB.BI)
Rendering service which renders reports locally

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.LocalBiRenderService, SanteDB.BI, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.BI.Services;
/// Other usings here
public class MyBiRenderService : SanteDB.BI.Services.IBiRenderService { 
	public String ServiceName => "My own IBiRenderService service";
	/// <summary>
	/// Render the specified report
	/// </summary>
	public System.IO.Stream Render(System.String reportId,System.String viewName,System.String formatName,System.Collections.Generic.IDictionary<System.String,System.Object> parameters,System.String& mimeType){
		throw new System.NotImplementedException();
	}
}
```
