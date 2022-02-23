---
description: >-
  Testing the Given Name textbox from Demographic Properties with multiple
  values.
---

# TEST: SECURITY-UM-13

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

New users being created can be assigned multiple given names in the **Given Name** textbox.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Select the **Given Name** textbox within the **Demographic Properties** section.

![](<../../../../../../../../.gitbook/assets/image (238).png>)

2\. Input a first name (e.g. "John") and press enter.

![](<../../../../../../../../.gitbook/assets/image (236).png>)

3\. Input a second name (e.g. "Jacob") and press enter.



## Expected Behaviour

* Each name entered should appear on an individual card inside the **Given Name** textbox.
* These steps can be repeated during user creation to add more names to the **Given Name** property.

![](<../../../../../../../../.gitbook/assets/image (234).png>)
