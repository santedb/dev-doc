---
description: >-
  Testing the addition of a Policy with Elevated Permission while editing a
  group's Assigned Policies.
---

# TEST: SECURITY-GRM-10

## References

* [Group / Role Management](../../../../../operations/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-08](test-security-grm-06.md)

## Discussion

After a **Policy** is added to the list of **Assigned Policies**, its **Permission** can be toggled to a value of **Elevate**.

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-GRM-08](test-security-grm-06.md) to create a group and assign a policy.

## Actions/Steps

1. Toggle **Permission** to **Elevate**, corresponding to the **Policy** having elevated permission**.**

![](../../../../../../.gitbook/assets/image%20%28374%29.png)

2. Click the **Save** button.

![](../../../../../../.gitbook/assets/image%20%28372%29.png)

## Expected Behaviour

* The **Permission** toggle button should switch to **Elevate** being darkened \(selected\) for the corresponding **Policy**.

![](../../../../../../.gitbook/assets/image%20%28375%29.png)

