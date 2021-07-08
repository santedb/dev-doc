---
description: Testing successful un-deletion of a user that has previously been deleted.
---

# TEST: SECURITY-UM-34

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-33](test-security-um-33-1.md)

## Discussion

After a user record has been deleted, it is not permanently destroyed. Deleted users can be **Un-Deleted** and is recovered from a Status of Obsolete in so doing. 

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-UM-33](test-security-um-33-1.md) to delete a user \(e.g. "ClinicalStaffUser123"\).

## Actions/Steps

1. While the **Show Deleted** button is toggled \(darkened\), deleted users can be un-deleted by clicking the **Un-Delete** button corresponding to the user to be recovered.

![](../../../../../../.gitbook/assets/image%20%28297%29.png)

2. Click the **OK** button on the confirmation modal that appears in the browser.

![](../../../../../../.gitbook/assets/image%20%28330%29.png)

## Expected Behaviour

* Table is reloaded to show un-deleted users and should include the user that was just reactivated \(e.g. "ClinicalStaffUser123"\).

![](../../../../../../.gitbook/assets/image%20%28324%29.png)

