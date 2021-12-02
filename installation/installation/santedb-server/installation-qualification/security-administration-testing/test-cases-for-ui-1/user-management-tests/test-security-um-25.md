---
description: Testing editing a User Profile by registering names for multiple Name Types.
---

# TEST: SECURITY-UM-25

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)
* [TEST: SECURITY-UM-13](test-security-um-13.md)
* [TEST: SECURITY-UM-14](test-security-um-14.md)

## Discussion

SanteSuite allows users to register multiple **Name** objects each with Prefix, Given, Family, and Suffix fields. Changing the **Name Type** for one of the Name Registration object form groups affects each form group heading.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1\. Click the **User Profile** tab.

![](<../../../../../../../.gitbook/assets/image (249).png>)

2\. Click the pencil in the top right-hand corner of the **Profile** to edit the properties.&#x20;

![](<../../../../../../../.gitbook/assets/image (272).png>)

3\. Click the **Add** button to start adding a new Name Registration form group.

![](<../../../../../../../.gitbook/assets/image (254).png>)

4\. Choose a different **Name Type** from the dropdown list (e.g. "Religious")

![](<../../../../../../../.gitbook/assets/image (244).png>)

5\. Select a **Suffix** and **Prefix** from the corresponding dropdown lists and enter any **Given** or **Family** name(s) similar to how it is done in [TEST: SECURITY-UM-13](test-security-um-13.md) and [TEST: SECURITY-UM-14](test-security-um-14.md).

![](<../../../../../../../.gitbook/assets/image (256).png>)

6\. Click the green checkmark to save the newly registered **Name** object.

![](<../../../../../../../.gitbook/assets/image (264).png>)

## Expected Behaviour

* Notice that **Remove** buttons appear below each form group when there is more than one.
* Notice that **Name Registration** form group headings change according to the selected **Name Type** after selecting from the dropdown in step 4.
* Notice the red circle with exclamation mark next to the **Name** tab in step 4 when a Name Registration form group is blank. Clicking the green checkmark like in step 6 without providing a **Name Type** first like in step 5 has a result of nothing occurring.
* A toast message appears in the top-right corner of the window stating "User updated successfully" when the steps above are followed correctly.

![](<../../../../../../../.gitbook/assets/image (269).png>)
