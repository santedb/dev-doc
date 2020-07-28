---
description: IMessagePersistenceService (SanteDB.Core.Api)
---

## Summary
Identifies a structure for message persistence service implementations

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetMessageState|SanteDB.Core.Services.MessageState|messageId <small style='border:solid 1px #aaa'>System.String</small>|Get the state of a message|
|PersistMessage|void|messageId <small style='border:solid 1px #aaa'>System.String</small><br/>message <small style='border:solid 1px #aaa'>System.IO.Stream</small>|Persists the message|
|PersistMessageInfo|void|message <small style='border:solid 1px #aaa'>SanteDB.Core.Services.MessageInfo</small>|Persist message extension|
|GetMessageResponseMessage|System.IO.Stream|messageId <small style='border:solid 1px #aaa'>System.String</small>|Get the identifier of the message that represents the response to the current message|
|GetMessage|System.IO.Stream|messageId <small style='border:solid 1px #aaa'>System.String</small>|Get a message|
|PersistResultMessage|void|messageId <small style='border:solid 1px #aaa'>System.String</small><br/>respondsToId <small style='border:solid 1px #aaa'>System.String</small><br/>response <small style='border:solid 1px #aaa'>System.IO.Stream</small>|Persist|
|GetMessageIds|System.Collections.Generic.IEnumerable&lt;System.String>|from <small style='border:solid 1px #aaa'>System.DateTime</small><br/>to <small style='border:solid 1px #aaa'>System.DateTime</small>|Get all message ids between the specified time(s)|
|GetMessageInfo|SanteDB.Core.Services.MessageInfo|messageId <small style='border:solid 1px #aaa'>System.String</small>|Get message extended attribute|

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
