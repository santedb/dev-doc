---
description: >-
  Testing the Username textbox from the Core Properties with a duplicate deleted
  user.
---

# TEST: SECURITY-UM-04

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-38](test-security-um-32.md) 

## Discussion

The Username textbox has UI that prevents Username re-use that is supportive of user un-deletion that is included within the architecture of SanteSuite. 

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. A deleted user must have been created previously with the name "ClinicalStaffUser123". See [TEST: SECURITY-UM-01](test-security-um-01.md) for user creation and [TEST: SECURITY-UM-38](test-security-um-32.md) for user deletion.
3. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1. Select the **Username** textbox within the **Core Properties** section.

![](../../../../../../.gitbook/assets/image%20%28210%29.png)

2. Enter a Username that is a duplicate of an existing deleted user in the **Username** textbox  \(e.g. "ClinicalStaffUser123" after [TEST: SECURITY-UM-01](test-security-um-01.md) and [TEST: SECURITY-UM-38](test-security-um-32.md)\).

## Expected Behaviour

* Red prompt should appear beneath the **Username** textbox stating, "duplicate record detected".
* User should not be created successfully by clicking save while all required **Security Properties** and **Demographic Properties** are provided with valid values.

![](../../../../../../.gitbook/assets/image%20%28229%29.png)

