`IClinicalProtocolRepositoryService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Contract for service implementations which store and manage definitions of [Protocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Protocol.htm)

## Description
Each protocol definition (stored in an instance of [Protocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Protocol.htm)) should be backed
            by an implementation of the [IClinicalProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Protocol_IClinicalProtocol.htm) interface. The primary responsibility of the [IClinicalProtocolRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IClinicalProtocolRepositoryService.htm)
            is to load these definitions from a user defined format (such as FHIR activity definitions, or the SanteDB XML CDSS format) and 
            generate the structured data which can be stored in the primary SanteDB database.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindProtocol|IEnumerable&lt;Protocol>|*Expression&lt;Func&lt;Protocol,Boolean>>* **predicate**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**|Find protocols in the repository service|
|InsertProtocol|Protocol|*Protocol* **data**|Find protocols in the repository service|

# Implementations


## Applet Based Clinical Protocol Repository - (SanteDB.Cdss.Xml)
Applet clinical protocol repository
### Description
This implementation of the [IClinicalProtocolRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IClinicalProtocolRepositoryService.htm) is responsible for loading 
            clinical protocols defined in [SanteDB's CDSS XML](https://help.santesuite.org/developers/applets/cdss-protocols) format and 
            translating them into [Protocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Protocol.htm) instances which can then, in-turn, be linked with instances of [Act](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Act.htm)
            which are also stored in the CDR.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Cdss.Xml.AppletClinicalProtocolRepository, SanteDB.Cdss.Xml, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyClinicalProtocolRepositoryService : SanteDB.Core.Services.IClinicalProtocolRepositoryService { 
	public String ServiceName => "My own IClinicalProtocolRepositoryService service";
	/// <summary>
	/// Find protocols in the repository service
	/// </summary>
	public IEnumerable<Protocol> FindProtocol(Expression<Func<Protocol,Boolean>> predicate,Int32 offset,Nullable<Int32> count,Int32& totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find protocols in the repository service
	/// </summary>
	public Protocol InsertProtocol(Protocol data){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IClinicalProtocolRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IClinicalProtocolRepositoryService.htm)
* [AppletClinicalProtocolRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Cdss_Xml_AppletClinicalProtocolRepository.htm)
