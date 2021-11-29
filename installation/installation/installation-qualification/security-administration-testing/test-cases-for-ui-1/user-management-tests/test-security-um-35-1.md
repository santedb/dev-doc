---
description: Testing the Lock button for an unlocked user.
---

# TEST: SECURITY-UM-35

## References

* [User Management](../../../../../../operations/system-administration/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)&#x20;

## Discussion

Users can be updated with a Status of Locked (for a maximum amount of time).

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating/deleting users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a user to be locked.
3. Navigate to **Administration Panel / Security / Users / Index**.

## Actions/Steps

1\.  Click the **Lock** button corresponding to a user with a Status of Active to be locked (e.g. "ClinicalStaffUser123").

![](<../../../../../../.gitbook/assets/image (300).png>)

2\. Click the **OK** button on the confirmation modal that appears in the browser.

![](<../../../../../../.gitbook/assets/image (334).png>)

## Expected Behaviour

* Status of the user that was unlocked changes to **Locked.**
* **Lock** button changes to an **Unlock** button.

![](<../../../../../../.gitbook/assets/image (330).png>)
