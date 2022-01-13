Localization Provider (ILocalizationService in SanteDB.Core.Api)

# Summary
Interface which provides localization functions

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetString|String|*String* **stringKey**|Get the specified string in the current locale|
|GetString|String|*String* **locale**<br/>*String* **stringKey**|Get the specified string in the current locale|
|FormatString|String|*String* **stringKey**<br/>*Object* **parameters**|Format a  with|
|FormatString|String|*String* **locale**<br/>*String* **stringKey**<br/>*Object* **parameters**|Format a  with|
|GetStrings|KeyValuePair`2[]|*String* **locale**|Get all strings in the specified locale|
|Reload|void||TODO|

# Implementations


## Applet Localization Service - (SanteDB.Core.Applets)
Applet localization

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletLocalizationService, SanteDB.Core.Applets, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyLocalizationService : SanteDB.Core.Services.ILocalizationService { 
	public String ServiceName => "My own ILocalizationService service";
	/// <summary>
	/// Get the specified string in the current locale
	/// </summary>
	public String GetString(String stringKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified string in the current locale
	/// </summary>
	public String GetString(String locale,String stringKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Format a  with
	/// </summary>
	public String FormatString(String stringKey,Object parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Format a  with
	/// </summary>
	public String FormatString(String locale,String stringKey,Object parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all strings in the specified locale
	/// </summary>
	public KeyValuePair`2[] GetStrings(String locale){
		throw new System.NotImplementedException();
	}
	public void Reload(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ILocalizationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ILocalizationService.htm)
* [AppletLocalizationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletLocalizationService.htm)
