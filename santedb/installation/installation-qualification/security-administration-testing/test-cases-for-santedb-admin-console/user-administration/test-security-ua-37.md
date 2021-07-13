---
description: >-
  Testing the user.roles command with non-existing username provided as -u
  parameter.
---

# TEST: SECURITY-UA-37

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.roles` command is for assigning roles to a user. 

* The `-u` parameter is used to specify the **username** of which user to assign roles to. 
* An exception is thrown when a non existing user is specified. 

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username does not exist.

## Actions/Steps

1. Execute the `user.roles` command with `-u` parameter specified as a non-existing username.

```text
user.roles -u <new user name>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text
> user.roles -u TestUser5678
ERR: Exception has been thrown by the target of an invocation.
        1:User TestUser5678 not found
```

