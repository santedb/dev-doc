---
description: >-
  Testing the Family Name textbox from Demographic Properties with multiple
  values.
---

# TEST: SECURITY-UM-14

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)&#x20;

## Discussion

New users being created can be assigned multiple family names in the **Family Name** textbox.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Select the **Family Name** textbox within the **Demographic Properties** section.

![](<../../../../../../../.gitbook/assets/image (245).png>)

2\. Input a first family name (e.g. "Jingleheimer") and press enter.

![](<../../../../../../../.gitbook/assets/image (246).png>)

3\. Input a second family name (e.g. "Schmidt") and press enter.

## Expected Behaviour

* Each name entered should appear on an individual card inside the **Family Name** textbox.
* These steps can be repeated during user creation to add more names to the **Family Name** property.

![](<../../../../../../../.gitbook/assets/image (247).png>)
