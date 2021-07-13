---
description: >-
  Testing the user.password command with existing username provided as -u
  parameter and with valid password provided as -p parameter.
---

# TEST: SECURITY-UA-35

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.password` command is for changing a specific users password. 

* The `-u` parameter is used to specify the **username** of which user's password to change. 
* The `-p`  parameter is used to specify a **password** that must pass strength validation.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.

## Actions/Steps

1. Execute the `user.password` command with `-u` parameter specified as an existing username and `-p` parameter specified as a sufficiently strong password.

```text
user.password -u demoadmin -p M0r3SeCuRe!
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text

```

