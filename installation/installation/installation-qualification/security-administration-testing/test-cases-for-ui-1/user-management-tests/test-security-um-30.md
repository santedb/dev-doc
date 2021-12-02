---
description: >-
  Testing appearance of the list of User object access Audit Events found while
  editing a specific user's properties within the Audit Trail tab.
---

# TEST: SECURITY-UM-30

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-21](test-security-um-21.md)

## Discussion

While editing a user account, the **Audit Trail** of events where the user object being edited was accessed can be reviewed and is represented by a table of Audit Events filtered based on user object access history.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-01](test-security-um-01.md) to create a new user -- applying any valid values for required fields.
3. Follow the instructions from [TEST: SECURITY-UM-21](test-security-um-21.md) to navigate to **Administration Panel / Security / Users / Edit User** for the newly created user.

## Actions/Steps

1\. Click on the **Audit Trail** tab.

![](<../../../../../../.gitbook/assets/image (313).png>)

## Expected Behaviour

* A table of Audit Events appears and is filtered to show events where the current user object was accessed.

![](<../../../../../../.gitbook/assets/image (305).png>)
