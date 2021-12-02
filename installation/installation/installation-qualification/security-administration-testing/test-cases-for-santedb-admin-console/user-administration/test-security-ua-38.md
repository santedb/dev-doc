---
description: >-
  Testing the user.roles command with existing username provided as -u parameter
  only.
---

# TEST: SECURITY-UA-38

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.roles` command is for assigning roles to a user.&#x20;

* The `-u` parameter is used to specify the **username** of which user to assign roles to.&#x20;
* An exception is thrown when no role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.

## Actions/Steps

1\. Execute the `user.roles` command with `-u` parameter specified as an existing user.

```
user.roles -u <existing username>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.roles -u TestUser123
ERR: Exception has been thrown by the target of an invocation.
        1:The specified roles do not exit. Roles are case sensitive
```
