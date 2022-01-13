`IBarcodeProviderService` in assembly SanteDB.Core.Api version 2.1.151.0

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
|Generate|Stream|*IEnumerable&lt;IdentifierBase&lt;TEntity>>* **identifers**|Generate a barcode from the specified identifier|
|Generate|Stream|*String* **rawData**|Generate the barcode from raw data|

# Implementations


## QR Code Barcode Generator - (SanteDB.DisconnectedClient.UI)
Barcode generator service that generates a QR code
### Description
This service is an implementation of the [IBarcodeProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBarcodeProviderService.htm) which generates 
            two dimensional barcodes with the ZXing library. This service uses the [IResourcePointerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IResourcePointerService.htm)
            to generate digitally signed [Visual Resource Pointer](https://help.santesuite.org/developers/service-apis/health-data-service-interface-hdsi/digitally-signed-visual-code-api) 
            payloads which are represented as a QR code.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.DisconnectedClient.UI.Services.QrBarcodeGenerator, SanteDB.DisconnectedClient.UI, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
	/// Generate a barcode from the specified identifier
	/// </summary>
	public Stream Generate<TEntity>(IEnumerable<IdentifierBase<TEntity>> identifers){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Generate the barcode from raw data
	/// </summary>
	public Stream Generate(String rawData){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IBarcodeProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBarcodeProviderService.htm)
* [QrBarcodeGenerator C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_DisconnectedClient_UI_Services_QrBarcodeGenerator.htm)
