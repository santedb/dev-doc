---
description: >-
  Testing the Updated By field from Core Properties in the Security tab before
  and after editing user properties.
---

# TEST: SECURITY-UM-22

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)
* [TEST: SECURITY-UM-06](test-security-um-06.md)

## Discussion

When a user's properties are edited, the user's corresponding **Updated By** core property is updated to the datetime edits are saved at.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User**.

## Actions/Steps

1\. Click the pencil in the top right-hand corner of **Security Properties** to edit them.&#x20;

![](<../../../../../../../../../.gitbook/assets/image (240).png>)

2\. Follow similar actions/steps from [TEST: SECURITY-UM-06](test-security-um-06.md) to add an additional role.

![](<../../../../../../../../../.gitbook/assets/image (216).png>)

3\.  Click the green checkmark to save the edited roles.

![](<../../../../../../../../../.gitbook/assets/image (252).png>)

4\. Refresh the page.

{% hint style="warning" %}
It is recommended to empty the cache and perform a hard reload in step 4.
{% endhint %}

## Expected Behaviour

* Notice that the users **Updated By** field in the **Core Properties** has changed to the datetime when roles were edited.

![Before editing.](<../../../../../../../../../.gitbook/assets/image (753).png>)

![After editing.](<../../../../../../../../../.gitbook/assets/image (76).png>)
