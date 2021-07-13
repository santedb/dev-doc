---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  and duplicate policy both denied and granted explicitly as -g and -d
  parameters.
---

# TEST: SECURITY-GRA-11

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md)
* [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) 

## Discussion

The `role.add` command is for adding new users and has 1 required parameter that must pass validation: **role**. 

* The `-r` parameter is used to specify which **role** to display information and effective policies from.
* The `-g` parameter is used to specify which **policy** to explicitly grant the new role being added.
* The `-d` parameter is used to specify which **policy** to explicitly deny the new role being added.
* An exception is thrown when a duplicate policy is both granted and denied in the same command.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.
3. See [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) for checking if a policy exists.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as non-existing role and with both `-d` and `-g` parameters specified as an identical existing policy.

```text
role.add -r <new role name> -d 1.3.6.1.4.1.33349.3.1.5.9.2.999 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999 
```

## Expected Behaviour

