---
description: Testing the user.del command with no parameters specified.
---

# TEST: SECURITY-UA-17

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.del` command is for de-activating users (effectively deleting the user) and has a single `-u` parameter for specifying **username** of user to delete.&#x20;

* An exception is thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.del` command.

```
user.del
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.del
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```
