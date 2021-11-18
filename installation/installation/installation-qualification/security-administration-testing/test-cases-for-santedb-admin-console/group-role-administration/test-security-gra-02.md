---
description: Testing the role.list command with -a flag specified.
---

# TEST: SECURITY-GRA-02

## References

* [Group / Role Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)

## Discussion

The `role.list` command is for listing groups/roles.&#x20;

* The `-a` flag is used to filter for **roles **that are de-activated (deleted).

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. There must be de-activated (deleted) roles see any roles listed in the expected behaviour for this specific test.

## Actions/Steps

1\. Execute the `role.list` command with the `-a` flag.

```
role.list -a
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```
> role.list -a
SID                                    Name                 Description                                      A
97ba3b52-811b-11eb-b733-00155d640b09   Test                 TEst
```

{% hint style="warning" %}
De-activated roles listed here may be outdated in the future and the list is subject to change.
{% endhint %}
