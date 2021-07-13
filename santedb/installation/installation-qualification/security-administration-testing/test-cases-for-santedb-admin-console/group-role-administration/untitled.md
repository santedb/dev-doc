---
description: Testing the role.add command with no parameters specified.
---

# TEST: SECURITY-GRA-06

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.add` command is for adding new users and has 1 required parameter that must pass validation: **role**. 

* An exception should be thrown when no parameters are specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `role.add` command.

```text
role.add
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text

```

