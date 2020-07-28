---
description: IBiRenderService (SanteDB.BI)
---

## Summary
BI Render service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Render|System.IO.Stream|reportId <small style='border:solid 1px #aaa'>System.String</small><br/>viewName <small style='border:solid 1px #aaa'>System.String</small><br/>formatName <small style='border:solid 1px #aaa'>System.String</small><br/>parameters <small style='border:solid 1px #aaa'>System.Collections.Generic.IDictionary<System.String,System.Object></small><br/>mimeType <small style='border:solid 1px #aaa'>System.String&</small>|Render the specified report|

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
