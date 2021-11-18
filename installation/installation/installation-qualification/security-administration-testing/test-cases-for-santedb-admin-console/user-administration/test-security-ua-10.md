---
description: Testing the user.add command with existing role with -r parameter only.
---

# TEST: SECURITY-UA-10

## References

* [User Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**.&#x20;

* The `-r` parameter is used to specify an existing **role **to assign to the user being newly added.&#x20;
* An exception should be thrown when no new username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role exists.

## Actions/Steps

1\. Execute the `user.add` command with `-r` parameter specified as an existing role.

```
user.add -r <existing role>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.add -r USERS
ERR: Exception has been thrown by the target of an invocation.
        1:Must specify a user
```
