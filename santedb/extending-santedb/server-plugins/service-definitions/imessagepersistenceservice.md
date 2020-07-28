---
description: IMessagePersistenceService (SanteDB.Core.Api)
---

# Message Persistence Service

## Summary

Identifies a structure for message persistence service implementations

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| GetMessageState | MessageState | _String_ **messageId** | Get the state of a message |
| PersistMessage | void | _String_ **messageId** _Stream_ **message** | Persists the message |
| PersistMessageInfo | void | _MessageInfo_ **message** | Persist message extension |
| GetMessageResponseMessage | Stream | _String_ **messageId** | Get the identifier of the message that represents the response to the current message |
| GetMessage | Stream | _String_ **messageId** | Get a message |
| PersistResultMessage | void | _String_ **messageId** _String_ **respondsToId** _Stream_ **response** | Persist |
| GetMessageIds | IEnumerable&lt;String&gt; | _DateTime_ **from** _DateTime_ **to** | Get all message ids between the specified time\(s\) |
| GetMessageInfo | MessageInfo | _String_ **messageId** | Get message extended attribute |

## Implementations

None

## Example Implementation

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

