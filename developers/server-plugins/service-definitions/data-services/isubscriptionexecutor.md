---
description: ISubscriptionExecutor (SanteDB.Core.Api)
---

# Data Subscription Execution

## Summary

Represents a subscription executor

## Events

| Event     | Type                                                  | Description           |
| --------- | ----------------------------------------------------- | --------------------- |
| Executed  | EventHandler\<QueryResultEventArgs\<IdentifiedData>>  | Occurs when queried.  |
| Executing | EventHandler\<QueryRequestEventArgs\<IdentifiedData>> | Occurs when querying. |

## Operations

| Operation | Response/Return      | Input/Parameter                                                                                                                                                                                                                                                                                                                    | Description                                   |
| --------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| Execute   | IEnumerable\<Object> | <p><em>Guid</em> <strong>subscriptionKey</strong><br><em>NameValueCollection</em> <strong>parameters</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong><br><em>Guid</em> <strong>queryId</strong></p>                | Executes the specified subscription mechanism |
| Execute   | IEnumerable\<Object> | <p><em>SubscriptionDefinition</em> <strong>subscription</strong><br><em>NameValueCollection</em> <strong>parameters</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong><br><em>Guid</em> <strong>queryId</strong></p> | Executes the specified subscription mechanism |

## Implementations

### ADO.NET Subscription Executor - (SanteDB.Persistence.Data.ADO)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoSubscriptionExector, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySubscriptionExecutor : SanteDB.Core.Services.ISubscriptionExecutor { 
    public String ServiceName => "My own ISubscriptionExecutor service";
    /// <summary>
    /// Occurs when queried.
    /// </summary>
    public event EventHandler<QueryResultEventArgs<IdentifiedData>> Executed;
    /// <summary>
    /// Occurs when querying.
    /// </summary>
    public event EventHandler<QueryRequestEventArgs<IdentifiedData>> Executing;
    /// <summary>
    /// Executes the specified subscription mechanism
    /// </summary>
    public IEnumerable<Object> Execute(Guid subscriptionKey,NameValueCollection parameters,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Executes the specified subscription mechanism
    /// </summary>
    public IEnumerable<Object> Execute(SubscriptionDefinition subscription,NameValueCollection parameters,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
        throw new System.NotImplementedException();
    }
}
```
