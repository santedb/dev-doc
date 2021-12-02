---
description: Testing the appearance of the modal viewed showing Audit Event Details.
---

# TEST: SECURITY-AR-01

## References

* [Audit Repository](../../../../../../operations/system-administration/security-administration/audit-repository.md)

## Discussion

The details of each event from the **Audit Repository** can be viewed.

## Pre-Conditions / Setup

1. Sign in with the "demoadmin" user or another user with permission to view **Audit Repository** events.
2. Navigate to the **Administration Panel / Security / Audit Log / List**.&#x20;

{% hint style="warning" %}
Entries in the table being filtered here are subject to change very frequently.
{% endhint %}

## Actions/Steps

&#x20;1\. Click on the **View** button corresponding to an Audit Event for which details need to be viewed.

![](<../../../../../../.gitbook/assets/image (379).png>)

## Expected Behaviour

* A modal with **Audit Event Details** should appear over the page with 4 panels (**Event Information**, **Network**, **Users & Computers**, and **Data & Objects**).

![](<../../../../../../.gitbook/assets/image (365).png>)
