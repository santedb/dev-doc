---
description: Testing the Name textbox with a duplicate deleted group.
---

# TEST: SECURITY-GRM-06

## References

* [Group / Role Management](../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-03](test-security-grm-03-1.md)

## Discussion

Groups cannot be created with a duplicate **Name** matching a deleted group.

## Pre-Conditions / Setup

1\. Follow instructions from [TEST: SECURITY-GRM-03](test-security-grm-03-1.md) to delete a group.

## Actions/Steps

1\. Click the **Create** button.

![](<../../../../../../.gitbook/assets/image (295).png>)

2\. Enter invalid **Name** for the group (duplicate; e.g. "Muddsville").

## Expected Behaviour

* No group should be created.
* Remain on **Administration Panel / Security / Groups / Create Group** page.
* Display a prompt below the required **Name** textbox with a validation message as follows:

![](<../../../../../../.gitbook/assets/image (328).png>)
