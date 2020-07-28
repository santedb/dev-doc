---
description: IMailMessageRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents an alerting service.

## Events

|Event|Type|Description|
|-|-|-|
|Committed|EventHandler&lt;MailMessageEventArgs>|Fired when an alert is received.|
|Received|EventHandler&lt;MailMessageEventArgs>|Fired when an alert was raised and is being processed.|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Broadcast|void|message <small style='border:solid 1px #aaa'>MailMessage</small>|Broadcasts an alert.|
|Find|IEnumerable&lt;MailMessage>|predicate <small style='border:solid 1px #aaa'>Expression<Func<MailMessage,Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>Int32&</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Searches for alerts.|
|Get|MailMessage|id <small style='border:solid 1px #aaa'>Guid</small>|Gets an alert.|
|Insert|MailMessage|message <small style='border:solid 1px #aaa'>MailMessage</small>|Inserts an alert message.|
|Save|MailMessage|message <small style='border:solid 1px #aaa'>MailMessage</small>|Saves an alert.|

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
