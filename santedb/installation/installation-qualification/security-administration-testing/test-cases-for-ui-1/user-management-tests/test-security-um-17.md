---
description: >-
  Testing deletion of a value within the Primary Facility textbox from
  Demographic Properties.
---

# TEST: SECURITY-UM-17

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-16](test-security-um-16.md)

## Discussion

When more than one **Primary Facility** is entered during user creation, individual **Primary Facility** values can be removed from **Demographic Properties** before submitting the form. 

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.
3. Follow [TEST: SECURITY-UM-16](test-security-um-16.md) to add multiple primary facilities to the **Primary Facility** textbox.

## Actions/Steps

1. Click the **x** on the left side of a **Primary Facility** tag that has been added to the **Primary Facility** textbox.

![](../../../../../../.gitbook/assets/image%20%28261%29.png)

## Expected Behaviour

* The **Primary Facility** tag corresponding to the **x** clicked is removed from the **Primary Facility** textbox.

![](../../../../../../.gitbook/assets/image%20%28250%29.png)

