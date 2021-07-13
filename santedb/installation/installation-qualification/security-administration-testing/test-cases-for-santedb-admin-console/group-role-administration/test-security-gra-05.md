---
description: Testing the role.info command with a existing role specified as -r parameter.
---

# TEST: SECURITY-GRA-05

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md) 

## Discussion

The `role.info` command is for listing a specific role's information and effective policies. The `-r` parameter is used to specify which **role** to display information and effective policies from.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role exists.

## Actions/Steps

1. Execute the `role.` command with `-r` parameter specified as an existing role.

```text
role.info -r <existing role name>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text

```

