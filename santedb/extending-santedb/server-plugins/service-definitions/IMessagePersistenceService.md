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
|GetMessageState|MessageState|messageId <small style='border:solid 1px #aaa'>String</small>|Get the state of a message|
|PersistMessage|void|messageId <small style='border:solid 1px #aaa'>String</small><br/>message <small style='border:solid 1px #aaa'>Stream</small>|Persists the message|
|PersistMessageInfo|void|message <small style='border:solid 1px #aaa'>MessageInfo</small>|Persist message extension|
|GetMessageResponseMessage|Stream|messageId <small style='border:solid 1px #aaa'>String</small>|Get the identifier of the message that represents the response to the current message|
|GetMessage|Stream|messageId <small style='border:solid 1px #aaa'>String</small>|Get a message|
|PersistResultMessage|void|messageId <small style='border:solid 1px #aaa'>String</small><br/>respondsToId <small style='border:solid 1px #aaa'>String</small><br/>response <small style='border:solid 1px #aaa'>Stream</small>|Persist|
|GetMessageIds|IEnumerable&lt;String>|from <small style='border:solid 1px #aaa'>DateTime</small><br/>to <small style='border:solid 1px #aaa'>DateTime</small>|Get all message ids between the specified time(s)|
|GetMessageInfo|MessageInfo|messageId <small style='border:solid 1px #aaa'>String</small>|Get message extended attribute|

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
	public MessageState GetMessageState(String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persists the message
	/// </summary>
	public void PersistMessage(String messageId,Stream message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persist message extension
	/// </summary>
	public void PersistMessageInfo(MessageInfo message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the identifier of the message that represents the response to the current message
	/// </summary>
	public Stream GetMessageResponseMessage(String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a message
	/// </summary>
	public Stream GetMessage(String messageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Persist
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
	/// Get message extended attribute
	/// </summary>
	public MessageInfo GetMessageInfo(String messageId){
		throw new System.NotImplementedException();
	}
}
```
