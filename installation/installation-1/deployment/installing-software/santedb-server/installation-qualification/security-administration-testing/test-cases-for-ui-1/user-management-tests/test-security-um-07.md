---
description: >-
  Testing successful removal of a role within the Role textbox from Security
  Properties.
---

# TEST: SECURITY-UM-07

## References

* [User Management](broken-reference)

## Discussion

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Follow [TEST: SECURITY-UM-06](test-security-um-06.md) to add multiple **Role Name** values to the **Role** textbox.

## Actions/Steps

1\. Click the **x** on the left side of a **Role Name** tag that has been added to the **Role** textbox.

![](../../../../../../../../../.gitbook/assets/Role\_RemoveHover.png)

## Expected Behaviour

* The **Role Name** tag corresponding to the **x** clicked is removed from the **Role** textbox.
* Only policies and permissions for the **Role Name(s)** in the **Role** textbox are applied upon creation of the corresponding user (see [TEST: SECURITY-UM-01](test-security-um-01.md)).

![](<../../../../../../../../../.gitbook/assets/image (52).png>)
