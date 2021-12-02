---
description: Testing the user.password command with no parameters specified.
---

# TEST: SECURITY-UA-32

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.password` command is for changing a specific users password.

* An exception is thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.password` command.

```
user.password
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.password
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```
