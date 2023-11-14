---
description: Testing the addition of a Member while editing a group's Members.
---

# TEST: SECURITY-GRM-13

## References

* [Group / Role Management](broken-reference)
* [TEST: SECURITY-GRM-01](test-security-grm-01-1.md)

## Discussion

A **Member** may be added to a group, to whom assigned policies are applied.

## Pre-Conditions / Setup

1. Follows the instructions from [TEST: SECURITY-GRM-01](test-security-grm-01-1.md) to create a group to be edited.
2. After a group is created, the user is automatically brought to the corresponding **Administration Panel / Security / Groups / Edit Group** page.

## Actions/Steps

1\. Select the **Add** dropdown within the **Members** panel.

![](<../../../../../../../../../.gitbook/assets/image (380).png>)

2\. Select a **Member** (e.g. "demoadmin") from the dropdown to be added to the list of **Members**.

![](<../../../../../../../../../.gitbook/assets/image (369).png>)

## Expected Behaviour

* The assigned **Member** (e.g. "demoadmin") is saved to the list of **Members**.
* Dropdown of policies in the **Add** field has its last selection cleared.

![](<../../../../../../../../../.gitbook/assets/image (355).png>)

{% hint style="info" %}
No need to click the **Save** button to updated the role successfully.
{% endhint %}
