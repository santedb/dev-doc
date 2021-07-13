---
description: >-
  Testing the user.add command with all required parameters (-r, -u, -p)
  specified with valid values.
---

# TEST: SECURITY-UA-14

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**. 

* The `-r` parameter is used to specify a role to assign to the user being newly added. 
* The `-u` parameter is used to specify a unique username to assign to the user being newly added. 
* The `-p`  parameter is used to specify a password that must pass strength validation.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role exists.
3. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a user does not exist.

## Actions/Steps

1. Execute the `user.add` command with the `-r` parameter specified as an existing role, `-u` parameter specified as a non-existing username, and `-u` parameter specified as sufficiently strong password.

```text
user.add -r USERS -u <new user name> -p M0r3SeCuRe!
```

## Expected Behaviour

