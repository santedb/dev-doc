---
description: >-
  Testing the filters for a user's Detailed Audit Log based on either Action,
  Event, or Outcome.
---

# TEST: SECURITY-UM-31

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-30](test-security-um-30.md)

## Discussion

A user's **Detailed Audit Log** may be filtered using 3 dropdowns to choose from static lists of ****a possible **Actions**, **Events**, or **Outcomes**.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-30](test-security-um-30.md) to navigate to the **Audit Trail** tab of a user's **Administration Panel / Security / Users / Edit User** page.

{% hint style="warning" %}
Entries in the table being filtered here are subject to change very frequently.
{% endhint %}

## Actions/Steps

1. Select any option from the **Actions** dropdown.

![](../../../../../../.gitbook/assets/image%20%28310%29.png)

2. Select any option from the **Events** dropdown.

![](../../../../../../.gitbook/assets/image%20%28299%29.png)

3. Select any option from the **Outcomes** dropdown.

![](../../../../../../.gitbook/assets/image%20%28292%29.png)

## Expected Behaviour

* The **Detailed Audit Log** table should be updated between each of steps 1, 2, and 3 to reflect the filter that has been applied.
* The final result should filter all 3 of the **Action**, **Event**, and **Outcome** columns. 

![](../../../../../../.gitbook/assets/image%20%28322%29.png)

