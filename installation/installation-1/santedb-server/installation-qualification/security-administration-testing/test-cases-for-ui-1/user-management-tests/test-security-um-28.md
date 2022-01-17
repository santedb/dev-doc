---
description: >-
  Testing editing User Profile textboxes from the Additional Info tab with valid
  values.
---

# TEST: SECURITY-UM-28

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)
* [TEST: SECURITY-UM-16](test-security-um-16.md)
* [TEST: SECURITY-UM-19](test-security-um-19.md)

## Discussion

SanteSuite user accounts can be edited&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1.Click the **User Profile** tab.

![](<../../../../../../../.gitbook/assets/image (265).png>)

2\. Click the pencil in the top right-hand corner of the **Profile** card to edit the properties.&#x20;

![](<../../../../../../../.gitbook/assets/image (272).png>)

3\. Click on the **Additional Info** tab.

![](<../../../../../../../.gitbook/assets/image (307).png>)

4\. Select or enter a **Birthdate** and enter any **Primary Facility** or **Employer** value(s) similar to how it is done in [TEST: SECURITY-UM-16](test-security-um-16.md) and [TEST: SECURITY-UM-19](test-security-um-19.md).

![](<../../../../../../../.gitbook/assets/image (315).png>)

5\. Click the green checkmark to save the **Contact Info** field(s) modified.

![](<../../../../../../../.gitbook/assets/image (264).png>)

## Expected Behaviour

* A toast message appears in the top-right corner of the window stating "User updated successfully" when the steps above are followed correctly.

![](<../../../../../../../.gitbook/assets/image (269).png>)

* The **Profile** card should be updated to show any changes to **Birthdate**, **Language(s)**, **Employer**, or **Primary Facility**.

![](<../../../../../../../.gitbook/assets/image (312).png>)
