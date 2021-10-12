---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  non-existing policy specified as -d parameter.
---

# TEST: SECURITY-GRA-13

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md)
* [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) 

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**. 

* The `-r` parameter is used to specify which **role** to display information and effective policies from.
* The `-d` parameter is used to specify which **policy **to explicitly deny the new role being added.
* An exception is thrown when a non-existing policy is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.
3. See [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) for checking if a policy exists.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as non-existing role and `-d` parameter specified as a non-existing policy.

```
role.add -r <new role name> -d 1234567890
```

## Expected Behaviour

//TODO: document test after bug is resolved for no exception thrown here.

* Admin Console output should appear similar to the following:

```
```
