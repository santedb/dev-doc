`ILocalizationService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Interface which provides localization functions

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetString|String|*String* **stringKey**|Get the specified string in the current locale|
|GetString|String|*String* **locale**<br/>*String* **stringKey**|Get the specified string in the current locale|
|GetString|String|*String* **stringKey**<br/>*Object* **parameters**|Get the specified string in the current locale|
|GetString|String|*String* **locale**<br/>*String* **stringKey**<br/>*Object* **parameters**|Get the specified string in the current locale|
|GetAvailableLocales|IEnumerable&lt;String>|*none*|TODO|
|GetStrings|IEnumerable&lt;KeyValuePair&lt;String,String>>|*String* **locale**|Get all strings in the specified locale|
|Reload|void|*none*|TODO|

# Implementations


## Applet Localization Service - (SanteDB.Core.Applets)
Applet localization

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletLocalizationService, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	/// Get the specified string in the current locale
	/// </summary>
	public String GetString(String stringKey,Object parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified string in the current locale
	/// </summary>
	public String GetString(String locale,String stringKey,Object parameters){
		throw new System.NotImplementedException();
	}
	public IEnumerable<String> GetAvailableLocales(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all strings in the specified locale
	/// </summary>
	public IEnumerable<KeyValuePair<String,String>> GetStrings(String locale){
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
