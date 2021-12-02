---
description: Testing the user.undel command with no parameters specified.
---

# TEST: SECURITY-UA-21

## References

* [User Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.undel` command is for re-activating de-activated users (effectively un-deleting the user) and has a single `-u` parameter for specifying **username** of user to un-delete.

* An exception is thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.undel`.

```
user.undel 
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.undel
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```
