---
description: Testing the user.add command with no parameters specified.
---

# TEST: SECURITY-UA-08

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**. 

* An exception should be thrown when no parameters are specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `user.add` command.

```text
user.add
```

## Expected Behaviour

*  Admin Console output should appear as follows:

```text
> user.add
ERR: Exception has been thrown by the target of an invocation.
        1:The specified roles do not exit. Roles are case sensitive
```

