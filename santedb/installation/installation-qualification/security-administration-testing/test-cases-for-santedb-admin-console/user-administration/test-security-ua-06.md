---
description: Testing the user.list command with the optional -a flag specified.
---

# TEST: SECURITY-UA-06

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.list` command is for listing users. 

* The `-a` parameter is used to filter users and show only **non-active** \(deleted\) users.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A user must be created and have status changed to non-active \(i.e. delete the user\) for testing the `-a` flag to show the non-active user.

## Actions/Steps

1. Execute the `user.list` command with the `-a` flag.

```text
user.list -a
```

## Expected Behaviour

