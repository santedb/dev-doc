---
description: >-
  Testing the Reset button for the Invalid Logins count from the Security
  Properties in the Security tab.
---

# TEST: SECURITY-UM-23

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)

## Discussion

The number of invalid login attempts per user is stored as a user's security property. This number can be edited only by resetting it to zero.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. User being tested must attempt to login with an incorrect password at least once.
4. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1\. Click the pencil in the top right-hand corner of **Security Properties** to edit them.

![](<../../../../../../../../../.gitbook/assets/image (684).png>)

2\. Click the **Reset** button beside the **Invalid Logins** property.

![](<../../../../../../../../../.gitbook/assets/image (197).png>)

3\. Click the **OK** button when the confirmation prompt appears in the browser.

![](<../../../../../../../../../.gitbook/assets/image (224).png>)

5\. Click the green checkmark to save the edited **Invalid Logins**.

![](<../../../../../../../../../.gitbook/assets/image (252).png>)

## Expected Behaviour

* After the **OK** button in step 3 is clicked, the changes do not get saved until after step 5 and will be undone if step 5 is not taken.
* The number of **Invalid Logins** is reset after step 3 and displays "0".
* After step 5, the number of invalid logins is saved.
