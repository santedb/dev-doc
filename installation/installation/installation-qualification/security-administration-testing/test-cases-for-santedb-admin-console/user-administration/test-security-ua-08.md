---
description: Testing the user.add command with no parameters specified.
---

# TEST: SECURITY-UA-08

## References

* [User Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**.&#x20;

* An exception should be thrown when no parameters are specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.add` command.

```
user.add
```

## Expected Behaviour

* &#x20;Admin Console output should appear as follows:

```
> user.add
ERR: Exception has been thrown by the target of an invocation.
        1:The specified roles do not exit. Roles are case sensitive
```
