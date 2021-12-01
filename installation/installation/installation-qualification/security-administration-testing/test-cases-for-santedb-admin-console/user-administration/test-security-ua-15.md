---
description: >-
  Testing the user.add command with all required parameters (-r, -u, -p)
  specified with valid values and optional -e parameter specified as invalid
  email.
---

# TEST: SECURITY-UA-15

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**.&#x20;

* The `-r` parameter is used to specify a **role** to assign to the user being newly added.&#x20;
* The `-u` parameter is used to specify a unique **username** to assign to the user being newly added.&#x20;
* The `-p`  parameter is used to specify a **password** that must pass strength validation.&#x20;
* The `-e`  parameter is used to specify an **email** for the new user being added.
* An exception should be thrown when an incorrectly formatted email is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role exists.
3. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username does not exist.

## Actions/Steps

1. Execute the `user.add` command with `-r` parameter specified as an existing role, `-u` parameter specified as a non-existing username, and `-u` parameter specified as sufficiently strong password. Add optional `-e` parameter with invalid email format.

```
user.add -r <existing role> -u <new user name> -p M0r3SeCuRe! -e <invalid email>
```

## Expected Behaviour

*
