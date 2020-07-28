---
description: ISubscriptionRepository (SanteDB.Core.Api)
---

# Data Subscription Management

## Summary

Represents an implementation of a repository which loads subscription definitions

## Implementations

None

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySubscriptionRepository : SanteDB.Core.Services.ISubscriptionRepository { 
    public String ServiceName => "My own ISubscriptionRepository service";
}
```

