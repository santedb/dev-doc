---
description: >-
  Testing the user.roles command with existing username provided as -u parameter
  and with valid role provided as -r parameter.
---

# TEST: SECURITY-UA-40

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)

## Discussion

The `user.roles` command is for assigning roles to a user. 

* The `-u` parameter is used to specify the **username** of which user to assign roles to. 
* The `-r` parameter is used to specify which **role** to assign to the specified user.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.
3. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role exists.

## Actions/Steps

1.  Execute the `user.roles` command with `-u` parameter specified as an existing user and `-r` parameter specified as an existing role.

```text
user.roles -u demoadmin -r USERS
```

## Expected Behaviour

