---
description: Testing the user.info command with no parameters specified.
---

# TEST: SECURITY-UA-25

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.info` command is for listing information about a user account and effective permissions with a single `-u` parameter for specifying a **username**.

* An exception is thrown when no parameter is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.info` command.

```
user.info
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.info
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```
