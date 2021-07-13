---
description: >-
  Testing the user.lock command with non-existing username provided as -u
  parameter only.
---

# TEST: SECURITY-UA-29

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.lock` command is for locking or unlocking existing users. 

* The `-u` parameter is used to specify a user to **unlock** whenever the `-l` flag is not specified.
* An exception is thrown when a non-existing user is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A user must be created and have status changed to non-active \(i.e. delete the user\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `user.` command with the `-` parameter specified as '&lt;&gt;'.

```text
user.lock -u <new user name>
```

## Expected Behaviour

