---
description: IBarcodeGeneratorService (SanteDB.Core.Api)
---

## Summary
Represents a barcode generator

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Generate|Stream|identifers <small style='border:solid 1px #aaa'>IEnumerable<IdentifierBase<TEntity>></small>|Generate a barcode from the specified identifier|

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
