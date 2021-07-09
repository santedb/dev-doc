---
description: >-
  Testing successfully editing the Description field from a group's Core
  Properties.
---

# TEST: SECURITY-GRM-07

## References

* [Group / Role Management](../../../../../operations/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-01](test-security-grm-01-1.md)

## Discussion

The **Decription** field is the only **Core Property** that can be edited for an existing group. ****

## Pre-Conditions / Setup

1. Follows the instructions from [TEST: SECURITY-GRM-01](test-security-grm-01-1.md) to create a group to be edited.
2. After a group is created, the user is automatically brought to the corresponding **Administration Panel / Security / Groups / Edit Group** page.

## Actions/Steps

1. Change the **Description** text area.

![](../../../../../../.gitbook/assets/image%20%28344%29.png)

2. Click the **Save** button.

![](../../../../../../.gitbook/assets/image%20%28372%29.png)

## Expected Behaviour

* Remain on **Administration Panel / Security / Groups / Edit Group** page.
* Changes are saved.
* Green toast appears briefly in top-right corner of window stating: "Role updated successfully".

![](../../../../../../.gitbook/assets/image%20%28378%29.png)

