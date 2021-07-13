---
description: Testing the user.lock command with no parameters specified.
---

# TEST: SECURITY-UA-28

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.lock` command is for locking or unlocking existing users. 

* An exception should be thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `user.lock` command.

```text
user.lock
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text
> user.lock
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```

