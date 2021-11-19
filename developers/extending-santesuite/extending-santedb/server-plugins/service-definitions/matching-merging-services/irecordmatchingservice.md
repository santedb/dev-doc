---
description: IRecordMatchingService (SanteDB.Core.Api)
---

# Record Matching Service

## Summary

Represents a service that performs record matching and classification

## Operations

| Operation | Response/Return                      | Input/Parameter                                                                                                                                                         | Description                                                                                                  |
| --------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Block     | IEnumerable\<T>                      | <p><em>T</em> <strong>input</strong><br><em>String</em> <strong>configurationName</strong></p>                                                                          | Instructs the record matching service to perform a quick block function of records            for type  with |
| Classify  | IEnumerable\<IRecordMatchResult\<T>> | <p><em>T</em> <strong>input</strong><br><em>IEnumerable&#x3C;T></em> <strong>blocks</strong><br><em>String</em> <strong>configurationName</strong></p>                  | Instructs the record matcher to run a detailed classification on the matching blocks in                      |
| Match     | IEnumerable\<IRecordMatchResult\<T>> | <p><em>T</em> <strong>input</strong><br><em>String</em> <strong>configurationName</strong></p>                                                                          | Instructs the record matcher to run a block and match operation against                                      |
| Score     | IRecordMatchResult\<T>               | <p><em>T</em> <strong>input</strong><br><em>Expression&#x3C;Func&#x3C;T,Boolean>></em> <strong>query</strong><br><em>String</em> <strong>configurationName</strong></p> | Performs a score against the specified query (how confident the match is that the  matches the               |

## Implementations

### SanteMatch Deterministic Matcher - (SanteDB.Matcher)

Represents a deterministic record matching service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Matcher.Matchers.SimpleRecordMatchingService, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### SanteMatch Probabalistic Match Service - (SanteDB.Matcher)

Represents a probabalistic record matching service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Matcher.Matchers.WeightedRecordMatchingService, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRecordMatchingService : SanteDB.Core.Services.IRecordMatchingService { 
    public String ServiceName => "My own IRecordMatchingService service";
    /// <summary>
    /// Instructs the record matching service to perform a quick block function of records            for type  with
    /// </summary>
    public IEnumerable<T> Block<T>(T input,String configurationName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Instructs the record matcher to run a detailed classification on the matching blocks in
    /// </summary>
    public IEnumerable<IRecordMatchResult<T>> Classify<T>(T input,IEnumerable<T> blocks,String configurationName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Instructs the record matcher to run a block and match operation against
    /// </summary>
    public IEnumerable<IRecordMatchResult<T>> Match<T>(T input,String configurationName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Performs a score against the specified query (how confident the match is that the  matches the
    /// </summary>
    public IRecordMatchResult<T> Score<T>(T input,Expression<Func<T,Boolean>> query,String configurationName){
        throw new System.NotImplementedException();
    }
}
```
