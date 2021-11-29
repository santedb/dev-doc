---
description: >-
  Testing the role.info command with a non-existing role specified as -r
  parameter.
---

# TEST: SECURITY-GRA-04

## References

* [Group / Role Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
*   [TEST: SECURITY-GRA-02](test-security-gra-02.md)&#x20;



## Discussion

The `role.info` command is for listing a specific role's information and effective policies.&#x20;

* The `-r` parameter is used to specify which **role** to display information and effective policies from.&#x20;
* An exception is thrown when an invalid (non-existing) role is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.

## Actions/Steps

1\. Execute the `role.info` command with `-r` parameter specified as a non-existing role.

```
role.info -r <non-existing role>
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```
> role.info -r not_a_role
ERR: Exception has been thrown by the target of an invocation.
        1:Role not_a_role not found
```

