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
|Render|Stream|*String* **reportId**<br/>*String* **viewName**<br/>*String* **formatName**<br/>*IDictionary<String,Object>* **parameters**<br/>*String&* **mimeType**|Render the specified report|

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
