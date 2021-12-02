---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  non-existing policy specified as -g parameter.
---

# TEST: SECURITY-GRA-12

## References

* [Group / Role Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md)
* [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md)&#x20;

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**.&#x20;

* The `-r` parameter is used to specify which **role** to display information and effective policies from.
* The `-g` parameter is used to specify which **policy** to explicitly grant the new role being added.
* An exception is thrown when a non-existing policy is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.
3. See [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) for checking if a policy exists.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as non-existing role and `-g` parameter specified as a non-existing policy.

```
role.add -r <new role name> -g 1234567890
```

## Expected Behaviour

//TODO: document test after bug is resolved for no exception thrown here.

* Admin Console output should appear similar to the following:

```
```
