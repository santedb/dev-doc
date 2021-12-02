---
description: >-
  Testing the addition of a Policy with Granted Permission while editing a
  group's Assigned Policies.
---

# TEST: SECURITY-GRM-08

## References

* [Group / Role Management](../../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-01](test-security-grm-01-1.md)

## Discussion

A **Policy** may be added to a group which is applied to group members.

## Pre-Conditions / Setup

1. Follows the instructions from [TEST: SECURITY-GRM-01](test-security-grm-01-1.md) to create a group to be edited.
2. After a group is created, the user is automatically brought to the corresponding **Administration Panel / Security / Groups / Edit Group** page.

## Actions/Steps

&#x20;1\. Select the **Add** dropdown within the **Assigned Policies** panel.

![](<../../../../../../../.gitbook/assets/image (351).png>)

2\. Select a **Policy** (e.g. "Create Local Users") from the dropdown to be added to the list of **Assigned Policies**.

![](<../../../../../../../.gitbook/assets/image (352).png>)

3\. Click on the plus sign (**+**) to add the selected policy.

![](<../../../../../../../.gitbook/assets/image (353).png>)

4\. Click the **Save** button after the selected **Policy** is added to the list of **Assigned Policies**.

![](<../../../../../../../.gitbook/assets/image (349).png>)

## Expected Behaviour

* The explicitly added **Policy** (e.g. "Create Local Users") is saved to the list of **Assigned Policies** with a **Permission** value of **Grant** selected by default (darkened button).
* Dropdown of policies in the **Add** field has its last selection cleared.

![](<../../../../../../../.gitbook/assets/image (354).png>)

* Green toast appears briefly in top-right corner of window stating: "Role updated successfully".

![](<../../../../../../../.gitbook/assets/image (350).png>)
