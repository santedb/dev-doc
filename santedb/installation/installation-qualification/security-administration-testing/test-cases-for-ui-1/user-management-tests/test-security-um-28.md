---
description: >-
  Testing editing User Profile textboxes from the Additional Info tab with valid
  values.
---

# TEST: SECURITY-UM-28

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)
* [TEST: SECURITY-UM-16](test-security-um-16.md)
* [TEST: SECURITY-UM-19](test-security-um-19.md)

## Discussion

SanteSuite user accounts can be edited 

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1.Click the **User Profile** tab.

![](../../../../../../.gitbook/assets/image%20%28265%29.png)

2. Click the pencil in the top right-hand corner of the **Profile** card to edit the properties. 

![](../../../../../../.gitbook/assets/image%20%28272%29.png)

3. Click on the **Additional Info** tab.

![](../../../../../../.gitbook/assets/image%20%28307%29.png)

4. Select or enter a **Birthdate** and enter any **Primary Facility** or **Employer** value\(s\) similar to how it is done in [TEST: SECURITY-UM-16](test-security-um-16.md) and [TEST: SECURITY-UM-19](test-security-um-19.md).

![](../../../../../../.gitbook/assets/image%20%28315%29.png)

5. Click the green checkmark to save the **Contact Info** field\(s\) modified.

![](../../../../../../.gitbook/assets/image%20%28264%29.png)

## Expected Behaviour

* A toast message appears in the top-right corner of the window stating "User updated successfully" when the steps above are followed correctly.

![](../../../../../../.gitbook/assets/image%20%28269%29.png)

* The **Profile** card should be updated to show any changes to **Birthdate**, **Language\(s\)**, **Employer**, or **Primary Facility**.

![](../../../../../../.gitbook/assets/image%20%28312%29.png)

