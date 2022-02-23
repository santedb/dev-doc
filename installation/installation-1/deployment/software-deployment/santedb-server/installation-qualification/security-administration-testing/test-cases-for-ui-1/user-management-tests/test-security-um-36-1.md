---
description: Testing the Unlock button for a locked user.
---

# TEST: SECURITY-UM-36

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-35](test-security-um-35-1.md)

## Discussion

Users with a Status of Locked can be updated with a Status of Active.

## Pre-Conditions / Setup

1. Follow instructions from [TEST: SECURITY-UM-35](test-security-um-35-1.md) to lock a user (e.g. "ClinicalStaffUser123").

## Actions/Steps

1\. Click on the **Unlock** button corresponding to the user meant to be unlocked (e.g. "ClinicalStyaffUser123").

![](<../../../../../../../../../.gitbook/assets/image (326).png>)

2\. Click the **OK** button in the confirmation modal that appears in the browser.

![](<../../../../../../../../../.gitbook/assets/image (332).png>)

## Expected Behaviour

* Status of the user that was locked changes to **Active.**
* **Unlock** button changes to a **Lock** button.

![](<../../../../../../../../../.gitbook/assets/image (298).png>)
