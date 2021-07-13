---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  and descripton/note provided as -n parameter.
---

# TEST: SECURITY-GRA-14

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.add` command is for adding new users and has 1 required parameter that must pass validation: **role**. 

* The `-r` parameter is used to specify which role to display information and effective policies from.
* The `-g` parameter is used to specify which policy to explicitly grant the new role being added.
* The `-d` parameter is used to specify which policy to explicitly deny the new role being added.
* The `-n` parameter is used to specify a description/note \(no spaces\). 

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A role must be created and have status changed to non-active \(i.e. delete the role\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified with a new role name and `-`**n** parameter specified with a special note for the new role.

```text
role.add -r <new role name> -n SPECIAL_ROLE_NOTE
```

## Expected Behaviour

