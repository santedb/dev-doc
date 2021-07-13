---
description: Testing the user.roles command with no parameters specified.
---

# TEST: SECURITY-UA-36

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.roles` command is for assigning roles to a user. 

* An exception is thrown when no parameters are specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `user.roles` command.

```text
user.roles
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text
> user.roles
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```

