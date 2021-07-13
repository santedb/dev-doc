---
description: Testing the user.list command with the optional -l flag specified.
---

# TEST: SECURITY-UA-07

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.list` command is for listing users. 

* The `-l` parameter is used to filter users and show only **locked** users.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. 
## Actions/Steps

1. Execute the `user.list` command with the `-l` flag.

```text
user.list -l
```

## Expected Behaviour

