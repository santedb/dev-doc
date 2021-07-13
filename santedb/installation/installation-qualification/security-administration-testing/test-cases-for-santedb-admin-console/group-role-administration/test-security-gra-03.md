---
description: Testing the role.info command with no parameters specified.
---

# TEST: SECURITY-GRA-03

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.info` command is for listing a specific role's information and effective policies with 1 required parameter that must pass validation: **role**. 

* An exception is thrown when no role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `role.info` command.

```text
role.info
```

## Expected Behaviour

