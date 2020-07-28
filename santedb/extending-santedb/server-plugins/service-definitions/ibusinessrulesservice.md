---
description: IBusinessRulesService<TModel> (SanteDB.Core.Api)
---

# Business Rules Service

## Summary

Represents a service that executes business rules based on triggers which happen in the persistence layer

### Remarks

Note: This can be done, instead with events on the persistence layer on the SanteDB datalayer, however there may come a time when a rule is fired without persistence occurring

## Properties

| Property | Type | Access | Description |
| :--- | :--- | :--- | :--- |
| Next | IBusinessRulesService&lt;TModel&gt; | RW | Gets or sets the rule to be run after this rule \(for chained rules\) |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| AfterInsert | TModel | _TModel_ **data** | Called after an insert occurs |
| AfterObsolete | TModel | _TModel_ **data** | Called after obsolete committed |
| AfterQuery | IEnumerable&lt;TModel&gt; | _IEnumerable&lt;TModel&gt;_ **results** | Called after query |
| AfterRetrieve | TModel | _TModel_ **result** | Called after retrieve |
| AfterUpdate | TModel | _TModel_ **data** | Called after update committed |
| BeforeInsert | TModel | _TModel_ **data** | Called before an insert occurs |
| BeforeObsolete | TModel | _TModel_ **data** | Called before obsolete |
| BeforeUpdate | TModel | _TModel_ **data** | Called before an update occurs |
| Validate | List&lt;DetectedIssue&gt; | _TModel_ **data** | Called to validate a specific object |

## Implementations

None

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyBusinessRulesService<TModel> : SanteDB.Core.Services.IBusinessRulesService<TModel> { 
    public String ServiceName => "My own IBusinessRulesService`1 service";
    /// <summary>
    /// Gets or sets the rule to be run after this rule (for chained rules)
    /// </summary>
    public IBusinessRulesService<TModel> Next {
        get;
        set;
    }
    /// <summary>
    /// Called after an insert occurs
    /// </summary>
    public TModel AfterInsert(TModel data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called after obsolete committed
    /// </summary>
    public TModel AfterObsolete(TModel data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called after query
    /// </summary>
    public IEnumerable<TModel> AfterQuery(IEnumerable<TModel> results){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called after retrieve
    /// </summary>
    public TModel AfterRetrieve(TModel result){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called after update committed
    /// </summary>
    public TModel AfterUpdate(TModel data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called before an insert occurs
    /// </summary>
    public TModel BeforeInsert(TModel data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called before obsolete
    /// </summary>
    public TModel BeforeObsolete(TModel data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called before an update occurs
    /// </summary>
    public TModel BeforeUpdate(TModel data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Called to validate a specific object
    /// </summary>
    public List<DetectedIssue> Validate(TModel data){
        throw new System.NotImplementedException();
    }
}
```

