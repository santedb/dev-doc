Audit Dispatch Provider (IAuditDispatchService in SanteDB.Core.Api)

# Summary
Represents a service that dispatches audits to a central repository

## Description
The auditing of access to clinical data is of the utmost importance. SanteDB generates 
            and stores audits locally using an [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) for [AuditData](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Auditing_AuditData.htm). However, 
            many implementations will have centralized audit repositories for collecting audits from various health
            systems in a central place. Such collection is useful to establishing overall patterns of access
            across systems in an HIE (for example)

The audit dispatching service is responsible for sending [AuditData](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Auditing_AuditData.htm) instances to remote
            audit repositories. The service's responsibilities are:

1. Ensure that the [AuditData](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Auditing_AuditData.htm) instance is complete and contains relevant information for this node
1. Transform the [AuditData](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Auditing_AuditData.htm) class into the appropriate format (IETF RFC3881, FHIR, etc.)
1. Ensure the delivery of the audit to the central repository

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|SendAudit|void|*AuditData* **audit**|Sends the audit to the central authority|

# Implementations


## IHE ATNA Audit Dispatcher - (SanteDB.Messaging.Atna)
Represents an audit service that communicates Audits via an IHE ATNA transport
### Description
This implementation of the [IAuditDispatchService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAuditDispatchService.htm) is responsible for 
            creating and dispatching audits in one of the appopriate formats for [IHE Audit Trail and Node Authentication](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html)
            audits.

The specific formats of audits supported are:

* [IETF RFC-3881](https://tools.ietf.org/html/rfc3881) messages
* [NEMA DICOM](https://dicom.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html) messages


The audits can be sent via a variety of transports including:

* UDP Syslog
* TCP Syslog
* Secure (TLS) TCP Syslog
* HTTP POST
* File System Settings


The configuration of this service is described in [AtnaConfigurationSection](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_Atna_Configuration_AtnaConfigurationSection.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.Atna.AtnaAuditService, SanteDB.Messaging.Atna, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## FhirAuditDispatcher - (SanteDB.Messaging.FHIR)
Audit dispatch service which sends audits using HL7 FHIR
### Description
This implementation of the [IAuditDispatchService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAuditDispatchService.htm) is responsible for dispatching audits to a central
            FHIR repository which supports the FHIR auditing specification.

This dispatcher is configured using the [FhirDispatcherTargetConfiguration](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_Configuration_FhirDispatcherTargetConfiguration.htm) class where the dispatcher name
            is ```audit```. The dispatcher configuration may include authentication/authorization parameters for the solution, as well
            as authenticators or proxy information.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.FHIR.Auditing.FhirAuditDispatcher, SanteDB.Messaging.FHIR, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAuditDispatchService : SanteDB.Core.Services.IAuditDispatchService { 
	public String ServiceName => "My own IAuditDispatchService service";
	/// <summary>
	/// Sends the audit to the central authority
	/// </summary>
	public void SendAudit(AuditData audit){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IAuditDispatchService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAuditDispatchService.htm)
* [AtnaAuditService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_Atna_AtnaAuditService.htm)
* [FhirAuditDispatcher C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_Auditing_FhirAuditDispatcher.htm)
