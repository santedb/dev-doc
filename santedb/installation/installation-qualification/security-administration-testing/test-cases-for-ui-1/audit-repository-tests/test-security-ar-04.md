---
description: >-
  Testing the filter for audit events based on either Event type, Action type,
  or Outcome type.
---

# TEST: SECURITY-AR-04

## References

* [User Management](../../../../../operations/security-administration/user-management.md)

## Discussion

A user's **Detailed Audit Log** may be filtered using 3 dropdowns to choose from static lists of** **a possible **Actions**, **Events**, or **Outcomes**.

## Pre-Conditions / Setup

1. Sign in with the "demoadmin" user or another user with permission to view **Audit Repository **events.
2. Navigate to the **Administration Panel / Security / Audit Log / List**.

{% hint style="warning" %}
Entries in the table being filtered here are subject to change very frequently.
{% endhint %}

## Actions/Steps

1\. Select any option from the **Actions** dropdown.

![](<../../../../../../.gitbook/assets/image (314).png>)

2\. Select any option from the **Events **dropdown.

![](<../../../../../../.gitbook/assets/image (301).png>)

3\. Select any option from the **Outcomes **dropdown.

![](<../../../../../../.gitbook/assets/image (294).png>)

## Expected Behaviour

* The **Audit Log** table should be updated between each of steps 1, 2, and 3 to reflect the filter that has been applied.
* The final result should filter all 3 of the **Action**, **Event**, and **Outcome** columns. 

![](<../../../../../../.gitbook/assets/image (357).png>)
