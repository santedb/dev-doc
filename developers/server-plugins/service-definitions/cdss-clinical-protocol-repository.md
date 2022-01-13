CDSS Clinical Protocol Repository (IClinicalProtocolRepositoryService in SanteDB.Core.Api)

# Summary
Represents a service that can do clinical protocols

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindProtocol|IEnumerable&lt;Protocol>|*Expression&lt;Func&lt;Protocol,Boolean>>* **predicate**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**|Find protocols in the repository service|
|InsertProtocol|Protocol|*Protocol* **data**|Find protocols in the repository service|

# Implementations


## Applet Based Clinical Protocol Repository - (SanteDB.Cdss.Xml)
Applet clinical protocol repository

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
