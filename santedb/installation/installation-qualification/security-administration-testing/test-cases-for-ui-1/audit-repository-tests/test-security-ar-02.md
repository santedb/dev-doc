---
description: >-
  Testing a User Name link to view a user from the Users & Computers section
  within Audit Event Details.
---

# TEST: SECURITY-AR-02

## References

* [Audit Repository](../../../../../operations/security-administration/audit-repository.md)
* [TEST: SECURITY-AR-01](test-security-ar-01.md)

## Discussion

When a user is an actor involved in an audit event, a link can be followed to that user from the **Audit Event Details**.

## Pre-Conditions / Setup

1. User must have permission to view the list of other users.
2. Follow the instructions from [TEST: SECURITY-AR-01](test-security-ar-01.md) to view the details of some **Audit Event** involving a user.

## Actions/Steps

1. Click on the **Users & Computers** accordion-panel heading.

![](../../../../../../.gitbook/assets/image%20%28371%29.png)

2. Click on a user's **User Name** appearing in the list of **Users & Computers** \(e.g. "demoadmin"\).

![](../../../../../../.gitbook/assets/image%20%28358%29.png)

## Expected Behaviour

* Automatically navigate to the **Administration Panel / Security / Users / Index** page.
* Automatically enter search string to show the user that was clicked.

![](../../../../../../.gitbook/assets/image%20%28354%29.png)

