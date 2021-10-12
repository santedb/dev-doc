---
description: >-
  Testing editing User Profile textboxes from the Contact Info tab with a valid
  value.
---

# TEST: SECURITY-UM-27

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)

## Discussion

SanteSuite user accounts can be edited to hold extended **Contact Info** that provides more than a single email and/or phone number.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User **for the newly created user.

## Actions/Steps

1\. Click the **User Profile **tab.

![](<../../../../../../.gitbook/assets/image (265).png>)

2\. Click the pencil in the top right-hand corner of the **Profile **card to edit the properties. 

![](<../../../../../../.gitbook/assets/image (272).png>)

3\. Click the **Contact info** tab.

![](<../../../../../../.gitbook/assets/image (286).png>)

4\. Click the toggle for an available Contact Info field to select either an email address or phone number and input the email address or phone number into the corresponding textbox.

![](<../../../../../../.gitbook/assets/image (289).png>)

5\. Click the green checkmark to save the **Contact Info **field(s) modified.

![](<../../../../../../.gitbook/assets/image (264).png>)

## Expected Behaviour

* A toast message appears in the top-right corner of the window stating "User updated successfully" when the steps above are followed correctly.

![](<../../../../../../.gitbook/assets/image (269).png>)

* The **Profile** card should be updated to show the new **Contact Info**.

![](<../../../../../../.gitbook/assets/image (288).png>)
