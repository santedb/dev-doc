---
description: >-
  Testing the user.add command with non-existing role provided as -r parameter
  only.
---

# TEST: SECURITY-UA-09

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**. 

* The `-r` parameter is used to specify an existing **role** to assign to the user being newly added. 
* An exception should be thrown when a non-existing role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role does not exist.

## Actions/Steps

1. Execute the `user.add` command with `-r` parameter specified as a non-existing role. 

```text
user.add -r <non-existing role>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text
> user.add -r not_a_role
ERR: Exception has been thrown by the target of an invocation.
        1:The specified roles do not exit. Roles are case sensitive
```

