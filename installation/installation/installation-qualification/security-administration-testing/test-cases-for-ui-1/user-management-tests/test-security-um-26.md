---
description: >-
  Testing editing a User Profile by registering multiple Addresses of different
  Address Type.
---

# TEST: SECURITY-UM-26

## References

* [User Management](../../../../../../operations/system-administration/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)

## Discussion

SanteSuite allows users to register multiple **Address** objects each with State/Province, Country/District, City, Precinct/Borough, Street, and Postal/ZIP fields. Changing the **Address Type** for one of the Address Registration object form groups affects each form group heading.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1\. Click the **User Profile** tab.

![](<../../../../../../.gitbook/assets/image (265).png>)

2\. Click the pencil in the top right-hand corner of the **Profile** to edit the properties.&#x20;

![](<../../../../../../.gitbook/assets/image (272).png>)

3\. Click the **Address** tab.

![](<../../../../../../.gitbook/assets/image (284).png>)

4\. By default, the "Home Address" **Address Type** is selected and blank. Enter valid address field values.

![](<../../../../../../.gitbook/assets/image (274).png>)

5\. Click the **Add** button in the bottom-right corner of the **Profile** to start adding a new Address Registration form group.

![](<../../../../../../.gitbook/assets/image (245).png>)

6\. Choose a different **Address Type** from the dropdown list (e.g. "Mailing Address").

![](<../../../../../../.gitbook/assets/image (259).png>)

7\. Enter valid **State/Province**, **Country/District**, **City**, **Precinct/Borough**, **Street**, and/or **Postal/ZIP** fields.

![](<../../../../../../.gitbook/assets/image (280).png>)

8\. Click the green checkmark to save the newly registered **Address** objects.

![](<../../../../../../.gitbook/assets/image (264).png>)

## Expected Behaviour

* Notice that **Remove** buttons appear below all but the first form group when there is more than one.
* Notice that **Address Registration** form group headings change according to the selected **Address Type** after selecting from the dropdown in step 6.
* Notice the red circle with exclamation mark next to the **Address** tab in step 6 when a Address Registration form group is blank. Clicking the green checkmark like in step 8 without providing a **Address Type** first like in step 6 has a result of nothing occurring.
* A toast message appears in the top-right corner of the window stating "User updated successfully" when the steps above are followed correctly.

![](<../../../../../../.gitbook/assets/image (269).png>)
