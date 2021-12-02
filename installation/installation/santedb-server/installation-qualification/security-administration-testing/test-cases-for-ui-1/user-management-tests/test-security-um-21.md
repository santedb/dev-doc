---
description: >-
  Testing that current Official Record (Suffix, Given Name(s), Family Name(s),
  Prefix)), Username, and Role(s) appear while editing user properties.
---

# TEST: SECURITY-UM-21

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

The top banner on the **Administrative Panel / Security / Users / Edit User** page should populate with the selected user's Official Record (Suffix, Given Name(s), Family Name(s), Prefix), Username, and Role(s).

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Navigate to **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Click the **Edit** button for an existing user (e.g. "ClinicalStaffUser123" from [TEST: SECURITY-UM-01](test-security-um-01.md)).

![](<../../../../../../../.gitbook/assets/image (260).png>)

## Expected Behaviour

* Banner displays Official Record (Suffix, Given Name(s), Family Name(s), Prefix), Username, and Role(s) for the user.
* If any Official Record (Suffix, Given Name(s), Family Name(s), Prefix), or Role(s) are edited, the banner should show these changes.

![](<../../../../../../../.gitbook/assets/image (261).png>)
