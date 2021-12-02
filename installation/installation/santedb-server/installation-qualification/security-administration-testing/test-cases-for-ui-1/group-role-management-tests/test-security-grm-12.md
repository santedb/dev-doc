---
description: Testing the removal of a member while editing a group's Members.
---

# TEST: SECURITY-GRM-14

## References

* [Group / Role Management](../../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-13](test-security-grm-11.md)

## Discussion

A **Member** is removable from a group.

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-GRM-13](test-security-grm-11.md) to create a group and assign a member.

## Actions/Steps

&#x20;1\. Click on the **Remove** button on a **Member** to be removed from a **Group/Role** that has been created.

![](<../../../../../../../.gitbook/assets/image (374).png>)

2\. Click the **OK** button on the confirmation prompt appearing in the browser.

![](<../../../../../../../.gitbook/assets/image (375).png>)

## Expected Behaviour

* The specific **Member** removed should not appear in the list after it is reloaded.

![](<../../../../../../../.gitbook/assets/image (378).png>)

*   Green toast appears briefly in top-right corner of window stating: "Role updated successfully".

    ![](<../../../../../../../.gitbook/assets/image (350).png>)

{% hint style="info" %}
No need to click the **Save** button to updated the role successfully.
{% endhint %}
