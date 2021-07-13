---
description: >-
  Testing the user.undel command with existing undeleted username provided as -u
  parameter.
---

# TEST: SECURITY-UA-24

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)
* [TEST: SECURITY-UA-27](test-security-ua-27.md)

## Discussion

The `user.undel` command is for re-activating de-activated users \(effectively un-deleting the user\) and has a single `-u` parameter for specifying username of user to un-delete.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.
3. See [TEST: SECURITY-UA-27](test-security-ua-27.md) for checking if a user is active \(un-deleted\).

## Actions/Steps

1. Execute the `user.undel` command with the `-u` parameter specified as an existing and undeleted username.

```text
user.undel -u <undeleted user>
```

## Expected Behaviour

