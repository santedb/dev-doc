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
|Render|Stream|reportId <small style='border:solid 1px #aaa'>String</small><br/>viewName <small style='border:solid 1px #aaa'>String</small><br/>formatName <small style='border:solid 1px #aaa'>String</small><br/>parameters <small style='border:solid 1px #aaa'>IDictionary<String,Object></small><br/>mimeType <small style='border:solid 1px #aaa'>String&</small>|Render the specified report|

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
	public Stream Render(String reportId,String viewName,String formatName,IDictionary<String,Object> parameters,String& mimeType){
		throw new System.NotImplementedException();
	}
}
```
