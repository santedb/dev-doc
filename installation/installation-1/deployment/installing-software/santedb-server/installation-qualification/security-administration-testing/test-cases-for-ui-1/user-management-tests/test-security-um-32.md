---
description: >-
  Testing the filters for User Activity based on either Action, Event, or
  Outcome while editing a user's account.
---

# TEST: SECURITY-UM-32

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-29](test-security-um-29.md)
* [TEST: SECURITY-UM-31](test-security-um-31.md)

## Discussion

A user's **User Activity** tab may be filtered using 3 dropdowns to choose from static lists of a possible **Actions**, **Events**, or **Outcomes**.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow the instructions from [TEST: SECURITY-UM-29](test-security-um-29.md) to navigate to the **User Activity** tab of a user's **Administration Panel / Security / Users / Edit User** page.

{% hint style="warning" %}
Entries in the table being filtered here are subject to change very frequently.
{% endhint %}

## Actions/Steps

1\. Follow similar instructions as [TEST: SECURITY-UM-31](test-security-um-31.md) except within the **User Activity** tab instead of the **Audit Trail** tab. Choose values from all 3 filter dropdowns.

## Expected Behaviour

* The **User Activity** table should be updated between each of steps 1, 2, and 3 to reflect the filter that has been applied.
* The final result should filter all 3 of the **Action**, **Event**, and **Outcome** columns.&#x20;

