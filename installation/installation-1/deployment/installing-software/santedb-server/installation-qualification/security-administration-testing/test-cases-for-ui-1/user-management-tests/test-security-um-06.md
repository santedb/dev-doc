---
description: Testing the Role textbox from Security Properties with multiple valid roles.
---

# TEST: SECURITY-UM-06

## References

* [User Management](broken-reference)
* [TEST: SECURITY-GRM-01](../group-role-management-tests/test-security-grm-01-1.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

Users can be assigned multiple roles/groups that could have various policies and permissions. A valid Role Name of an existing Group must be searched one at a time as each is entered and/or selected within a single textbox.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Multiple **Role Names** corresponding to groups must exist to assign to a user (see [TEST: SECURITY-GRM-01](../group-role-management-tests/test-security-grm-01-1.md) for successful Group creation).
3. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Select the **Role** textbox within the **Security Properties** section.

![](<../../../../../../../../../.gitbook/assets/image (701).png>)

2\. Click on an existing group's **Role Name** in the dropdown menu (e.g. "USERS" has been selected here).

![](<../../../../../../../../../.gitbook/assets/image (713).png>)

3\. Begin entering the string value of another existing group's **Role Name** until it is the only matching **Role Name** appearing in the dropdown menu (e.g. "sensi" is being entered here and only matches "SENSITIVE\_USERS" as intended).

![](<../../../../../../../../../.gitbook/assets/image (722).png>)

4\. Press the **Enter** key.

## Expected Behaviour

* Multiple tags appear, each representing a **Role Name** of a group and can be removed from the **Role** textbox.
* Policies and permissions for the **Role Name(s)** in the **Role** textbox are applied upon creation of the corresponding user (see [TEST: SECURITY-UM-01](test-security-um-01.md)).

![](<../../../../../../../../../.gitbook/assets/image (772).png>)
