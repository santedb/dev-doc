---
description: >-
  Testing the user.lock command with existing username provided as -u parameter
  and without -l flag.
---

# TEST: SECURITY-UA-30

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.lock` command is for locking or unlocking existing users.

* The `-u` parameter is used to specify a user to **unlock** whenever the `-l` flag is not specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.

## Actions/Steps

1. Execute the `user.lock` command with `-u` parameter specified as an existing username.

```text
user.lock -u demoadmin
```

## Expected Behaviour

