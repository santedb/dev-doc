---
description: Testing the user.undel command with no parameters specified.
---

# TEST: SECURITY-UA-21

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.undel` command is for re-activating de-activated users \(effectively un-deleting the user\) and has a single `-u` parameter for specifying username of user to un-delete.

* An exception is thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `user.undel`.

```text
user.undel 
```

## Expected Behaviour

