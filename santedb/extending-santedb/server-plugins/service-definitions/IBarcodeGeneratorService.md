---
description: IBarcodeGeneratorService (SanteDB.Core.Api)
---

## Summary
Represents a barcode generator

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Generate|Stream|*IEnumerable&lt;IdentifierBase&lt;TEntity>>* **identifers**|Generate a barcode from the specified identifier|

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
	public Stream Generate<TEntity>(IEnumerable<IdentifierBase<TEntity>> identifers){
		throw new System.NotImplementedException();
	}
}
```
