---
description: Testing the user.lock command with no parameters specified.
---

# TEST: SECURITY-UA-28

## References

* [User Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.lock` command is for locking or unlocking existing users.&#x20;

* An exception should be thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.lock` command.

```
user.lock
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.lock
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```
