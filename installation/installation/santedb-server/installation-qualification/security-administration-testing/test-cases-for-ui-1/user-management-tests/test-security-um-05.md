---
description: Testing the Role textbox from Security Properties with an invalid value.
---

# TEST: SECURITY-UM-05

## References

* [User Management](broken-reference)

## Discussion

Users can be assigned multiple roles/groups that could have various policies and permissions. An invalid Role Name is one that is not a Core Property of any Group.&#x20;

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. **Role Name** of the group being entered/added to a user's roles must not exist.
3. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Select the **Role** textbox within the **Security Properties** section.

![](<../../../../../../../.gitbook/assets/image (228).png>)

2\. Enter a string that does not match the **Role Name** for any existing group **** (e.g. "NOT\_A\_ROLE" is being entered here and role names are searched as each character is modified).&#x20;

![](<../../../../../../../.gitbook/assets/image (71).png>)

## Expected Behaviour

* The dropdown of possible matching Role Names should display a single disabled value only to prompt the user that there are "no results found".
* The non-existent role being searched should not be added to the **Role** textbox (in this case it remains blank when no other values are present).

![](<../../../../../../../.gitbook/assets/image (85).png>)
