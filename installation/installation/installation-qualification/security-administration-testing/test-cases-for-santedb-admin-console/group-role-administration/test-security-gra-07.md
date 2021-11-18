---
description: Testing the role.add command with existing role provided as -r parameter only.
---

# TEST: SECURITY-GRA-07

## References

* [Group / Role Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md)&#x20;

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**.&#x20;

* The `-r` parameter is used to specify which **role **to display information and effective policies from.
* An exception should be thrown when an invalid (non-existing) role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role exists.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as an existing role.

```
role.add -r <existing role name>
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```
```
