---
description: >-
  Testing the New/Confirm Password textboxes for mismatching passwords from
  Security Properties.
---

# TEST: SECURITY-UM-10

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* &#x20;[TEST: SECURITY-UM-02](test-security-um-02.md)

## Discussion

A new password and confirmation password must match to be accepted as valid during user creation or password reset.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Enter "Clinic@l123" in the **New Password** textbox.

2\. Enter any string not matching "Clinic@l123" in the **Confirm Password** textbox.

## Expected Behaviour

* A red error message should appear below the **Confirm Password** textbox stating that "passwords must match".&#x20;

![](<../../../../../../../../../.gitbook/assets/image (74).png>)

* Nothing should occur if all other required fields are provided valid values and the **Save** button is clicked (see [TEST: SECURITY-UM-01](test-security-um-01.md) for successful creation and [TEST: SECURITY-UM-02](test-security-um-02.md) for required fields missing).

![](<../../../../../../../../../.gitbook/assets/image (134).png>)
