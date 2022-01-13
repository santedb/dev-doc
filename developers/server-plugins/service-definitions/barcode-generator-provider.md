Barcode Generator Provider (IBarcodeProviderService in SanteDB.Core.Api)

# Summary
Represents a barcode generator

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Generate|Stream|*IEnumerable&lt;IdentifierBase&lt;TEntity>>* **identifers**|Generate a barcode from the specified identifier|
|Generate|Stream|*String* **rawData**|Generate the barcode from raw data|

# Implementations


## QR Code Barcode Generator - (SanteDB.DisconnectedClient.UI)
Barcode generator service that generates a QR code

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
