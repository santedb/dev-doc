`IMailMessageService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which handles the mailbox services.

# Events

|Event|Type|Description|
|-|-|-|
|Sent|EventHandler&lt;MailMessageEventArgs>|Fired when an mail message has been received.|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Send|MailMessage|*MailMessage* **mail**|Send the specified mailmessage according to its sending instructions|
|GetMailboxes|IQueryResultSet&lt;Mailbox>|*Nullable&lt;Guid>* **forUserKey**|Get mailboxes for the current user|
|GetMailbox|Mailbox|*String* **mailboxName**|Get a specific mailbox|
|CreateMailbox|Mailbox|*String* **name**<br/>*Nullable&lt;Guid>* **ownerKey**|Create a new mailbox for the specified user|
|GetMessages|IQueryResultSet&lt;MailboxMailMessage>|*String* **mailboxName**|Get messages from the mailbox|
|MoveMessage|MailboxMailMessage|*Guid* **messageKey**<br/>*String* **targetMailboxName**<br/>*Boolean* **copy**|Move  to|
|DeleteMessage|MailboxMailMessage|*String* **fromMailboxName**<br/>*Guid* **messageKey**|Delete the specified message|
|DeleteMailbox|Mailbox|*String* **fromMailboxName**<br/>*Nullable&lt;Guid>* **ownerKey**|Delete mailbox from current user account|
|UpdateStatusFlag|MailboxMailMessage|*Guid* **mailMessageKey**<br/>*MailStatusFlags* **statusFlag**|Update the flag for the specified mail message instance|

# Implementations


## LocalMailMessageService - (SanteDB.Core.Api)
Represents a [IMailMessageService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IMailMessageService.htm) which uses database persistence layer 
            to store / retrieve mail messages within the system

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalMailMessageService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyMailMessageService : SanteDB.Core.Services.IMailMessageService { 
	public String ServiceName => "My own IMailMessageService service";
	/// <summary>
	/// Fired when an mail message has been received.
	/// </summary>
	public event EventHandler<MailMessageEventArgs> Sent;
	/// <summary>
	/// Send the specified mailmessage according to its sending instructions
	/// </summary>
	public MailMessage Send(MailMessage mail){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get mailboxes for the current user
	/// </summary>
	public IQueryResultSet<Mailbox> GetMailboxes(Nullable<Guid> forUserKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a specific mailbox
	/// </summary>
	public Mailbox GetMailbox(String mailboxName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a new mailbox for the specified user
	/// </summary>
	public Mailbox CreateMailbox(String name,Nullable<Guid> ownerKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get messages from the mailbox
	/// </summary>
	public IQueryResultSet<MailboxMailMessage> GetMessages(String mailboxName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Move  to
	/// </summary>
	public MailboxMailMessage MoveMessage(Guid messageKey,String targetMailboxName,Boolean copy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete the specified message
	/// </summary>
	public MailboxMailMessage DeleteMessage(String fromMailboxName,Guid messageKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete mailbox from current user account
	/// </summary>
	public Mailbox DeleteMailbox(String fromMailboxName,Nullable<Guid> ownerKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Update the flag for the specified mail message instance
	/// </summary>
	public MailboxMailMessage UpdateStatusFlag(Guid mailMessageKey,MailStatusFlags statusFlag){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IMailMessageService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IMailMessageService.htm)
* [LocalMailMessageService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_LocalMailMessageService.htm)
