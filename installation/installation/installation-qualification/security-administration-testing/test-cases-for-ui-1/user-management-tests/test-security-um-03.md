---
description: >-
  Testing the Username textbox from the Core Properties with a duplicate
  non-deleted user.
---

# TEST: SECURITY-UM-03

## References

* [User Management](../../../../../../operations/system-administration/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-39](test-security-um-34-1.md)

## Discussion

The Username textbox has UI that prevents Username re-use that is supportive of user un-deletion included within the architecture of SanteSuite.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. A non-deleted user must have been created previously with the name "ClinicalStaffUser123". See [TEST: SECURITY-UM-01](test-security-um-01.md) for user creation or [TEST: SECURITY-UM-39](test-security-um-34-1.md) for user un-deletion.
3. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Select the **Username** textbox within the **Core Properties** section.

![](<../../../../../../.gitbook/assets/image (210).png>)

2\. Enter a Username that is a duplicate of an existing un-deleted user in the **Username** textbox  (e.g. "ClinicalStaffUser123" after [TEST: SECURITY-UM-01](test-security-um-01.md)).

## Expected Behaviour

* Red prompt should appear beneath the **Username** textbox stating, "duplicate record detected".
* User should not be created successfully by clicking save while all required **Security Properties** and **Demographic Properties** are provided with valid values.

![](<../../../../../../.gitbook/assets/image (229).png>)
