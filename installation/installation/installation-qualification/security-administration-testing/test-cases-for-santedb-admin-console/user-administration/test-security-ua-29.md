---
description: >-
  Testing the user.lock command with non-existing username provided as -u
  parameter only.
---

# TEST: SECURITY-UA-29

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.lock` command is for locking or unlocking existing users.&#x20;

* The `-u` parameter is used to specify a **username** of the user to **unlock** only if `-l` flag is not specified.
* An exception is thrown when a non-existing user is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username does not exist.

## Actions/Steps

1\. Execute the `user.lock` command with `-u` parameter specified as a non-existing username.

```
user.lock -u <new user name>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
>> user.lock -u TestUser5678
ERR: Exception has been thrown by the target of an invocation.
        1:User TestUser5678 not found
```
