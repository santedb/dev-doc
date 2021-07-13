---
description: >-
  Testing the role.info command with a non-existing role specified as -r
  parameter.
---

# TEST: SECURITY-GRA-04

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.info` command is for listing a specific role's information and effective policies. 

* The `-r` parameter is used to specify which role to display information and effective policies from. 
* An exception is thrown when an invalid \(non-existing\) role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A role must be created and have status changed to non-active \(i.e. delete the role\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `role.` command with the `-` parameter specified as '&lt;&gt;'.

```text
role.info -r not_a_role
```

## Expected Behaviour



