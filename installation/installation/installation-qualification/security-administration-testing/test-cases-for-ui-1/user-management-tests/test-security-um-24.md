---
description: >-
  Testing the Reset Password prompt by successfully resetting a user's password
  from the Security Properties in the Security tab.
---

# TEST: SECURITY-UM-24

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)
* [TEST: SECURITY-UM-08](test-security-um-08.md)

## Discussion

A user's password can be reset by editing their Security Properties.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1\. Click the pencil in the top right-hand corner of **Security Properties** to edit them.

![](<../../../../../../.gitbook/assets/image (253).png>)

2\. Click the **Reset Pwd** button.

![](<../../../../../../.gitbook/assets/image (276).png>)

3\. Enter a **New Password** and a matching **Confirm Password** that is either **Strong** or **Very Strong** (see [TEST: SECURITY-UM-08](test-security-um-08.md)) and click the **Save** button.

![](<../../../../../../.gitbook/assets/image (281).png>)

## Expected Behaviour

* A toast message appears in the top-right corner of the window stating that password changes have been saved.
* There is no need to click the green checkmark in the top-right corner of **Security Properties** for the password changes to be saved.

![](<../../../../../../.gitbook/assets/image (277).png>)
