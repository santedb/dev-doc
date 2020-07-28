---
description: IMailMessageRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents an alerting service.

## Events

|Event|Type|Description|
|-|-|-|
|Committed|System.EventHandler&lt;SanteDB.Core.Mail.MailMessageEventArgs>|Fired when an alert is received.|
|Received|System.EventHandler&lt;SanteDB.Core.Mail.MailMessageEventArgs>|Fired when an alert was raised and is being processed.|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Broadcast|void|message <small style='border:solid 1px #aaa'>SanteDB.Core.Mail.MailMessage</small>|Broadcasts an alert.|
|Find|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Mail.MailMessage>|predicate <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Mail.MailMessage,System.Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>System.Int32&</small><br/>orderBy <small style='border:solid 1px #aaa'>SanteDB.Core.Model.Query.ModelSort`1[[SanteDB.Core.Mail.MailMessage, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null]][]</small>|Searches for alerts.|
|Get|SanteDB.Core.Mail.MailMessage|id <small style='border:solid 1px #aaa'>System.Guid</small>|Gets an alert.|
|Insert|SanteDB.Core.Mail.MailMessage|message <small style='border:solid 1px #aaa'>SanteDB.Core.Mail.MailMessage</small>|Inserts an alert message.|
|Save|SanteDB.Core.Mail.MailMessage|message <small style='border:solid 1px #aaa'>SanteDB.Core.Mail.MailMessage</small>|Saves an alert.|

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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyMailMessageRepositoryService : SanteDB.Core.Services.IMailMessageRepositoryService { 
	public String ServiceName => "My own IMailMessageRepositoryService service";
	/// <summary>
	/// Fired when an alert is received.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Mail.MailMessageEventArgs> Committed;
	/// <summary>
	/// Fired when an alert was raised and is being processed.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Mail.MailMessageEventArgs> Received;
	/// <summary>
	/// Broadcasts an alert.
	/// </summary>
	public void Broadcast(SanteDB.Core.Mail.MailMessage message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Searches for alerts.
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Mail.MailMessage> Find(System.Linq.Expressions.Expression<System.Func<SanteDB.Core.Mail.MailMessage,System.Boolean>> predicate,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalCount,SanteDB.Core.Model.Query.ModelSort`1[[SanteDB.Core.Mail.MailMessage, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null]][] orderBy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets an alert.
	/// </summary>
	public SanteDB.Core.Mail.MailMessage Get(System.Guid id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts an alert message.
	/// </summary>
	public SanteDB.Core.Mail.MailMessage Insert(SanteDB.Core.Mail.MailMessage message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Saves an alert.
	/// </summary>
	public SanteDB.Core.Mail.MailMessage Save(SanteDB.Core.Mail.MailMessage message){
		throw new System.NotImplementedException();
	}
}
```
