---
description: >-
  Testing the unsuccessful assigning of a policy to an object ( device or
  application or role ) when using policy name instead of policy OID.
---

# TEST: SECURITY-PA-06

## References

* [Policy Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/policy-administration.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when assigning policies to a role specifying a policy name instead of policy OID.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**policy.assign**" command followed by "**-d" (**or** "--device") **followed** **by the device(s) to assign the policy to followed by "**-p**" (or "**--policy**") followed by the policy(ies) name(s) to apply. (for example "Create-Policy-Test"

```
> policy.assign -d Create-Device-Test -p Create-Policy-Test
```

## Expected Behaviour

1- Should display an error message indicating that policy could not be found.

```
> policy.assign -d Create-Device-Test -p Create-Policy-Test
ERR: Exception has been thrown by the target of an invocation.
        1:Could not find one or more policies
>
```
