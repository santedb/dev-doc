`IMessagePersistenceService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Identifies a service which maintains a log of messages received to ensure that actions are only processed once

## Description
In a health context, certain types of messages which represent data triggers (such as an admit, discharge, order, etc.) may trigger 
            a business process which, in turn, kicks off another business process. Sometimes this process can take a long time to complete, or
            (due to network issues) the caller may disconnect prior to receiving a response. This service is responsible for storing that 
            a message has been received by the SanteDB infrastructure and is currently being (or was already) processed, and allows SanteDB
            to simply return the already executed message back to the caller.
            

Note: This service is only currently used by the HL7v2 service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetMessageState|MessageState|*String* **messageId**|Get the current state of a message processing by the unique identifier of the message|
|PersistMessage|void|*String* **messageId**<br/>*Stream* **message**|Instructs the message persistence service to store an inbound message|
|PersistMessageInfo|void|*MessageInfo* **message**|Persist metadata about the message|
|GetMessageResponseMessage|Stream|*String* **messageId**|Get the response to the supplied request message identifier|
|GetMessage|Stream|*String* **messageId**|Get a message body by message identifier|
|PersistResultMessage|void|*String* **messageId**<br/>*String* **respondsToId**<br/>*Stream* **response**|Persist the result of a message request (i.e. the result of the request)|
|GetMessageIds|IEnumerable&lt;String>|*DateTime* **from**<br/>*DateTime* **to**|Get all message ids between the specified time(s)|
|GetMessageInfo|MessageInfo|*String* **messageId**|Get message extended attributes|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyMessagePersistenceService : SanteDB.Core.Services.IMessagePersistenceService { 
	public String ServiceName => "My own IMessagePersistenceService service";
	/// <summary>
	/// Get the current state of a message processing by the unique identifier of the message
	/// </summary>
	public MessageState GetMessageState(String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the message persistence service to store an inbound message
	/// </summary>
	public void PersistMessage(String messageId,Stream message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persist metadata about the message
	/// </summary>
	public void PersistMessageInfo(MessageInfo message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the response to the supplied request message identifier
	/// </summary>
	public Stream GetMessageResponseMessage(String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a message body by message identifier
	/// </summary>
	public Stream GetMessage(String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persist the result of a message request (i.e. the result of the request)
	/// </summary>
	public void PersistResultMessage(String messageId,String respondsToId,Stream response){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all message ids between the specified time(s)
	/// </summary>
	public IEnumerable<String> GetMessageIds(DateTime from,DateTime to){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get message extended attributes
	/// </summary>
	public MessageInfo GetMessageInfo(String messageId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IMessagePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IMessagePersistenceService.htm)
