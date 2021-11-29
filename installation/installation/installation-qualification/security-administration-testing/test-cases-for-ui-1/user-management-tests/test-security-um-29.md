---
description: >-
  Testing appearance of the list of Audit Events found while editing a specific
  user's properties within the User Activity tab.
---

# TEST: SECURITY-UM-29

## References

* [User Management](../../../../../../operations/system-administration/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)

## Discussion

While editing a user account, the **User Activity** can be reviewed and is represented by a table of  Audit Events filtered based on the user being edited.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1\. Click the **User Activity** tab.

![](<../../../../../../.gitbook/assets/image (337).png>)

## Expected Behaviour

* A table of Audit Events appears and is filtered to show events involving the user being edited (based on user activity).

![](<../../../../../../.gitbook/assets/image (299).png>)
