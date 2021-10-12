---
description: Testing the Search field for Audit Events.
---

# TEST: SECURITY-AR-05

## References

* [Audit Repository](../../../../../operations/security-administration/audit-repository.md)

## Discussion

The **Audit Log **can be filtered using a Search string matching substrings of any **Actor** involved

## Pre-Conditions / Setup

1. Sign in with the "demoadmin" user or another user with permission to view **Audit Repository **events.
2. Navigate to the **Administration Panel / Security / Audit Log / List**. 

{% hint style="warning" %}
Entries in the table being filtered here are subject to change very frequently.
{% endhint %}

## Actions/Steps

1\. Select the search bar at the top-right corner of the **Administration Panel / Security / Audit Log / List** page.

![](<../../../../../../.gitbook/assets/image (385).png>)

2\. Enter an actor's name (**User**/**Device**) that appears in the Audit Log.

## Expected Behaviour

* The table of audit events should be filtered to show only those involving the actor being searched.

![](<../../../../../../.gitbook/assets/image (366).png>)
