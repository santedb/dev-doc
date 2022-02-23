---
description: Testing the Reset Password button and prompt for a user.
---

# TEST: SECURITY-UM-37

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-24](test-security-um-24.md)

## Discussion

A user's password can be reset by accessing a modal from the Users list.

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user who's password will be reset (e.g. "ClinicalStaffUser123").
2. Navigate to **Administration Panel / Security / Users / Index**.&#x20;

## Actions/Steps

1\. Click the **Reset Pwd** button corresponding to the user whos password is being reset (e.g. "ClinicalStaffUser123").

![](<../../../../../../../../.gitbook/assets/image (323).png>)

## Expected Behaviour

* A modal appears for resetting a user's password.&#x20;
* Can reset the user's password by referring to step 3 of [TEST: SECURITY-UM-24](test-security-um-24.md) and supply valid **New/Confirm** **Passwords** in a similar password reset modal.

![](<../../../../../../../../.gitbook/assets/image (290).png>)
