---
description: Testing the successful deletion of a group.
---

# TEST: SECURITY-GRM-03

## References

* [Group / Role Management](broken-reference)
* [TEST: SECURITY-GRM-01](test-security-grm-01-1.md)

## Discussion

SanteSuite groups cannot be permanently destroyed. Deleting a group means that it is moved to a list of deleted groups.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating/deleting groups.
2. Follow the instructions from [TEST: SECURITY-UM-01](../user-management-tests/test-security-um-01.md) to create a group to be deleted.
3. Navigate to **Administration Panel / Security / Groups / Index**.

## Actions/Steps

&#x20;1\. Click the **Delete** button in the same row as the group to be deleted.

![](<../../../../../../../../../.gitbook/assets/image (524).png>)

2\. Click the **OK** button on the confirmation prompt that appears in the browser.

![](<../../../../../../../../../.gitbook/assets/image (540).png>)

## Expected Behaviour

* Deleted group should be removed from the list after it reloads and is added to the list of deleted groups.
* Clicking the **Show Deleted** button should toggle (darkened button) the list of deleted groups and should include the group that was just deleted (e.g. "Muddsville" in this case).

![](<../../../../../../../../../.gitbook/assets/image (202).png>)
