---
description: >-
  Testing the user.roles command with existing username provided as -u parameter
  and with invalid role provided as -r parameter.
---

# TEST: SECURITY-UA-39

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)

## Discussion

The `user.roles` command is for assigning roles to a user.&#x20;

* The `-u` parameter is used to specify the **username** of which user to assign roles to.
* The `-r` parameter is used to specify which **role** to assign to the specified user.
* An exception is thrown when an invalid (non-existing) role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.
3. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role does not exist.

## Actions/Steps

1\. Execute the `user.roles` command with `-u` parameter specified as an existing user and `-r` parameter specified as a non-existing role.

```
user.roles -u <existing username> -r <non-existing role>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.roles -u TestUser123 -r not_a_role
ERR: Exception has been thrown by the target of an invocation.
        1:The specified roles do not exit. Roles are case sensitive
```
