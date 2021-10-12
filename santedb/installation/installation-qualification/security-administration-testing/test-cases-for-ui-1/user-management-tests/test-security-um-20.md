---
description: >-
  Testing deletion of a value within the Employer textbox from Demographic
  Properties.
---

# TEST: SECURITY-UM-20

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-19](test-security-um-19.md)

## Discussion

When more than one **Employer** is entered during user creation, individual **Employer** values can be removed from **Demographic Properties **before submitting the form. 

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.
3. Follow [TEST: SECURITY-UM-19](test-security-um-19.md) to add multiple primary facilities to the **Primary Facility** textbox.

## Actions/Steps

1\. Click the **x** on the left side of a **Employer** tag that has been added to the **Employer** textbox.

![](<../../../../../../.gitbook/assets/image (268).png>)

## Expected Behaviour

* The **Employer** tag corresponding to the **x** clicked is removed from the **Employer **textbox.

![](<../../../../../../.gitbook/assets/image (263).png>)
