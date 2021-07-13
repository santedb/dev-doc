---
description: Testing the role.list command with -a flag specified.
---

# TEST: SECURITY-GRA-02

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.list` command is for listing groups/roles. 

* The `-a` flag is used to filter for **roles** that are de-activated \(deleted\).

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. There must be de-activated \(deleted\) roles see any roles listed in the expected behaviour for this specific test.

## Actions/Steps

1. Execute the `role.list` command with the `-a` flag.

```text
role.list -a
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text

```

