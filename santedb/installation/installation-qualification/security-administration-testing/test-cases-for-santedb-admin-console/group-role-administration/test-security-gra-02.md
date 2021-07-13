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

* The `-a` flag is used to filter for roles that are de-activated \(deleted\).

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A role must be created and have status changed to non-active \(i.e. delete the role\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `role.` command with the `-` parameter specified as '&lt;&gt;'.

```text
role.list -a
```

## Expected Behaviour

