---
description: >-
  Testing the user.del command with non-existing username provided as -u
  parameter only.
---

# TEST: SECURITY-UA-18

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.del` command is for de-activating users (effectively deleting the user) and has a single `-u` parameter for specifying **username **of user to delete. 

* An exception is thrown when a non-existing username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username does not exist.

## Actions/Steps

1\. Execute the `user.del` command with `-u` parameter specified as a new username.

```
user.del -u <new user name>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.del -u not_a_user
ERR: Exception has been thrown by the target of an invocation.
        1:User not_a_user not found
```
