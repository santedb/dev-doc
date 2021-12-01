---
description: Testing the removal of a Policy while editing a group's Assigned Policies.
---

# TEST: SECURITY-GRM-11

## References

* [Group / Role Management](../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-08](test-security-grm-06.md)

## Discussion

A **Policy** is removable from a group.

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-GRM-08](test-security-grm-06.md) to create a group and assign a policy.

## Actions/Steps

1\. Click the **Remove** button corresponding to the **Policy** to be removed.

![](<../../../../../../.gitbook/assets/image (381).png>)

2\. Click the **OK** button on the confirmation prompt appearing briefly in the browser.

![](<../../../../../../.gitbook/assets/image (367).png>)

## Expected Behaviour

* The specific **Policy** removed should not appear in the list after it is reloaded.

![](<../../../../../../.gitbook/assets/image (368).png>)
