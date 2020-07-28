---
description: IBarcodeGeneratorService (SanteDB.Core.Api)
---

## Summary
Represents a barcode generator

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Api.Services;
/// Other usings here
public class MyBarcodeGeneratorService : SanteDB.Core.Api.Services.IBarcodeGeneratorService { 
	public String ServiceName => "My own IBarcodeGeneratorService service";
	/// <summary>
	/// Generate a barcode from the specified identifier
	/// </summary>
	public System.IO.Stream Generate<TEntity>(System.Collections.Generic.IEnumerable<SanteDB.Core.Model.DataTypes.IdentifierBase<TEntity>> identifers){
		throw new System.NotImplementedException();
	}
}
```
