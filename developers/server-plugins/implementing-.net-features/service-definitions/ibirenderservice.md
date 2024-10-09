`IBiRenderService` in assembly SanteDB.BI version 3.0.1980.0

# Summary
BI Render service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Render|Stream|*String* **reportId**<br/>*String* **viewName**<br/>*String* **formatName**<br/>*IDictionary&lt;String,Object>* **parameters**<br/>*String&* **mimeType**|Render the specified report|

# Implementations


## LocalBiRenderService - (SanteDB.BI)
Rendering service which renders reports locally

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BI.Services.Impl.LocalBiRenderService, SanteDB.BI, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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

# References

* [IBiRenderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_IBiRenderService.htm)
* [LocalBiRenderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BI_Services_Impl_LocalBiRenderService.htm)
