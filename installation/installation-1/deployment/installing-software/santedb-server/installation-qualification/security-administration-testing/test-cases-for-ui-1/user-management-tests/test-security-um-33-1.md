---
description: Testing the successful deletion of a user.
---

# TEST: SECURITY-UM-33

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)&#x20;

## Discussion

SanteSuite users cannot be permanently destroyed. Deleting a user means that it is moved to a list of deleted users.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating/deleting users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a user to be deleted.
3. Navigate to **Administration Panel / Security / Users / Index**.

## Actions/Steps

1\. Click the **Delete** button in the same row as the user to be deleted.

![](<../../../../../../../../../.gitbook/assets/image (714).png>)

2\. Click the **OK** button on the confirmation modal that appears in the browser.

![](<../../../../../../../../../.gitbook/assets/image (225).png>)

## Expected Behaviour

* Deleted user should be removed from the list after it reloads and is added to the list of deleted users.
* Clicking the **Show Deleted** button should toggle (darkened button) the list of deleted users and should include the user that was just deleted (e.g. "ClinicalStaffUser123" in this case).

![](<../../../../../../../../../.gitbook/assets/image (543).png>)
