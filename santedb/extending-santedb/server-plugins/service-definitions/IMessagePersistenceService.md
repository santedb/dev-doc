---
description: IMessagePersistenceService (SanteDB.Core.Api)
---

## Summary
Identifies a structure for message persistence service implementations

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyMessagePersistenceService : SanteDB.Core.Services.IMessagePersistenceService { 
	public String ServiceName => "My own IMessagePersistenceService service";
	/// <summary>
	/// Get the state of a message
	/// </summary>
	public SanteDB.Core.Services.MessageState GetMessageState(System.String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persists the message
	/// </summary>
	public void PersistMessage(System.String messageId,System.IO.Stream message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persist message extension
	/// </summary>
	public void PersistMessageInfo(SanteDB.Core.Services.MessageInfo message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the identifier of the message that represents the response to the current message
	/// </summary>
	public System.IO.Stream GetMessageResponseMessage(System.String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a message
	/// </summary>
	public System.IO.Stream GetMessage(System.String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persist
	/// </summary>
	public void PersistResultMessage(System.String messageId,System.String respondsToId,System.IO.Stream response){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all message ids between the specified time(s)
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.String> GetMessageIds(System.DateTime from,System.DateTime to){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get message extended attribute
	/// </summary>
	public SanteDB.Core.Services.MessageInfo GetMessageInfo(System.String messageId){
		throw new System.NotImplementedException();
	}
}
```
