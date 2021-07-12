---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  and a policy denied explicitly.
---

# TEST: SECURITY-GRA-10

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.` command is for &lt;&gt; and the `-` parameter is used to &lt;&gt;.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A role must be created and have status changed to non-active \(i.e. delete the role\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `role.` command with the `-` parameter specified as '&lt;&gt;'.

```text
role. -
```

## Expected Behaviour

