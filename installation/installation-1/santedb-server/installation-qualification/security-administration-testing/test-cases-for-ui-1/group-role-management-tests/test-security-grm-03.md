---
description: Testing the Name textbox with a duplicate non-deleted group.
---

# TEST: SECURITY-GRM-05

## References

* [Group / Role Management](broken-reference)
* [TEST: SECURITY-GRM-01](test-security-grm-01-1.md)

## Discussion

Groups cannot be created with a duplicate **Name** matching an un-deleted group.

## Pre-Conditions / Setup

1. Follow instructions from [TEST: SECURITY-GRM-01](test-security-grm-01-1.md) to create a new group.
2. Navigate to **Administration Panel / Security / Groups / Index**.&#x20;

## Actions/Steps

1\. Click the **Create** button.

![](<../../../../../../../.gitbook/assets/image (295).png>)

2\. Enter invalid **Name** for the group (duplicate; e.g. "Muddsville").

## Expected Behaviour

* No group should be created.
* Remain on **Administration Panel / Security / Groups / Create Group** page.
* Display a prompt below the required **Name** textbox with a validation message as follows:

![](<../../../../../../../.gitbook/assets/image (328).png>)
