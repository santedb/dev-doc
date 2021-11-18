---
description: IMailMessageRepositoryService (SanteDB.Core.Api)
---

# Mail Repository

## Summary

Represents an alerting service.

## Events

| Event     | Type                                | Description                                            |
| --------- | ----------------------------------- | ------------------------------------------------------ |
| Committed | EventHandler\<MailMessageEventArgs> | Fired when an alert is received.                       |
| Received  | EventHandler\<MailMessageEventArgs> | Fired when an alert was raised and is being processed. |

## Operations

| Operation | Response/Return           | Input/Parameter                                                                                                                                                                                                                                                                                     | Description               |
| --------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| Broadcast | void                      | _MailMessage_ **message**                                                                                                                                                                                                                                                                           | Broadcasts an alert.      |
| Find      | IEnumerable\<MailMessage> | <p><em>Expression&#x3C;Func&#x3C;MailMessage,Boolean>></em> <strong>predicate</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalCount</strong><br><em>ModelSort`1[]</em> <strong>orderBy</strong></p> | Searches for alerts.      |
| Get       | MailMessage               | _Guid_ **id**                                                                                                                                                                                                                                                                                       | Gets an alert.            |
| Insert    | MailMessage               | _MailMessage_ **message**                                                                                                                                                                                                                                                                           | Inserts an alert message. |
| Save      | MailMessage               | _MailMessage_ **message**                                                                                                                                                                                                                                                                           | Saves an alert.           |

## Implementations

### Local Mail Message - (SanteDB.Core)

Represents a local alert service.

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalMailMessageRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyMailMessageRepositoryService : SanteDB.Core.Services.IMailMessageRepositoryService { 
    public String ServiceName => "My own IMailMessageRepositoryService service";
    /// <summary>
    /// Fired when an alert is received.
    /// </summary>
    public event EventHandler<MailMessageEventArgs> Committed;
    /// <summary>
    /// Fired when an alert was raised and is being processed.
    /// </summary>
    public event EventHandler<MailMessageEventArgs> Received;
    /// <summary>
    /// Broadcasts an alert.
    /// </summary>
    public void Broadcast(MailMessage message){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Searches for alerts.
    /// </summary>
    public IEnumerable<MailMessage> Find(Expression<Func<MailMessage,Boolean>> predicate,Int32 offset,Nullable<Int32> count,Int32& totalCount,ModelSort`1[] orderBy){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets an alert.
    /// </summary>
    public MailMessage Get(Guid id){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Inserts an alert message.
    /// </summary>
    public MailMessage Insert(MailMessage message){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Saves an alert.
    /// </summary>
    public MailMessage Save(MailMessage message){
        throw new System.NotImplementedException();
    }
}
```
