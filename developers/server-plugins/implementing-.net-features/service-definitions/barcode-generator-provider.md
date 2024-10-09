`IBarcodeProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a barcode generator (QR, CODE39, etc.) which generates visual pointers to provided data

## Description
The barcode generator provider is responsible for accepting one or more [EntityIdentifier](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_DataTypes_EntityIdentifier.htm) or 
            [ActIdentifier](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_DataTypes_ActIdentifier.htm) instances from an object, and generating a secure barcode which points at the provided 
            resource. Additionally, the barcode provider provides SanteDB with the tooling to generate barcodes from raw data. 
            These barcodes should be returned as an appropriate stream (containing PNG, PDF, or other data) which can be served
            to the other SanteDB components such as BI reports, or the REST API

This interface is the basis for the [Visual Resource Pointer](https://help.santesuite.org/developers/service-apis/health-data-service-interface-hdsi/digitally-signed-visual-code-api) API

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetBarcodeGenerator|IBarcodeGenerator|*String* **barcodeAlgorithm**|Get the  for|

# Implementations


## DefaultBarcodeProviderService - (SanteDB.Core.Api)
Default implementation of [IBarcodeProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBarcodeProviderService.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultBarcodeProviderService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyBarcodeProviderService : SanteDB.Core.Services.IBarcodeProviderService { 
	public String ServiceName => "My own IBarcodeProviderService service";
	/// <summary>
	/// Get the  for
	/// </summary>
	public IBarcodeGenerator GetBarcodeGenerator(String barcodeAlgorithm){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBarcodeProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBarcodeProviderService.htm)
* [DefaultBarcodeProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_DefaultBarcodeProviderService.htm)
