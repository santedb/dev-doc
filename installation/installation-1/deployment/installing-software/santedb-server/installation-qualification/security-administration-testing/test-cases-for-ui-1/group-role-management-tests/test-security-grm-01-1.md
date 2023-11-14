---
description: Testing the successful creation of a Group with all properties specified.
---

# TEST: SECURITY-GRM-01

## References

* [Group / Role Management](broken-reference)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating new groups on the [Group / Role Management](broken-reference) page.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating groups.
2. Navigate to **Administration Panel / Security / Groups / Index**.&#x20;

## Actions/Steps

1\. Click the **Create** button.

![](<../../../../../../../../../.gitbook/assets/image (699).png>)

2\. Enter a valid **Name** for the group (non-duplicate).

![](<../../../../../../../../../.gitbook/assets/image (589).png>)

3\. Optionally enter a **Description** (max. 2048 characters).

![](<../../../../../../../../../.gitbook/assets/image (226).png>)

4\. Click the **Save** button.

![](<../../../../../../../../../.gitbook/assets/image (88).png>)

## Expected Behaviour

* Green toast appears briefly in top-right corner of window stating: "Role updated successfully".

![](<../../../../../../../../../.gitbook/assets/image (114).png>)

* Page is redirected to **Administration Panel / Security / Groups / Edit Group** for the new group create successfully.

![](<../../../../../../../../../.gitbook/assets/image (241).png>)
