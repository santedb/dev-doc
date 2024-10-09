`IGeographicLocationProvider` in assembly SanteDB.Client version 3.0.1980.0

# Summary
Represents a geo-tagging service to get device and position

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetCurrentPosition|GeoTag|*none*|TODO|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Client.Services;
/// Other usings here
public class MyGeographicLocationProvider : SanteDB.Client.Services.IGeographicLocationProvider { 
	public String ServiceName => "My own IGeographicLocationProvider service";
	public GeoTag GetCurrentPosition(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IGeographicLocationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Services_IGeographicLocationProvider.htm)
