---
description: >-
  Testing the addition of a Policy with Elevated Permission while editing a
  group's Assigned Policies.
---

# TEST: SECURITY-GRM-10

## References

* [Group / Role Management](../../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-08](test-security-grm-06.md)

## Discussion

After a **Policy** is added to the list of **Assigned Policies**, its **Permission** can be toggled to a value of **Elevate**.

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-GRM-08](test-security-grm-06.md) to create a group and assign a policy.

## Actions/Steps

1\. Toggle **Permission** to **Elevate**, corresponding to the **Policy** having elevated permission**.**

![](<../../../../../../../.gitbook/assets/image (359).png>)

2\. Click the **Save** button.

![](<../../../../../../../.gitbook/assets/image (349).png>)

## Expected Behaviour

* The **Permission** toggle button should switch to **Elevate** being darkened (selected) for the corresponding **Policy**.

![](<../../../../../../../.gitbook/assets/image (358).png>)
