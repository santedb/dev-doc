---
description: >-
  Testing the Search textbox for querying policies while editing a group's
  Assigned Policies.
---

# TEST: SECURITY-GRM-12

## References

* [Group / Role Management](../../../../../operations/security-administration/group-role-management.md)

## Discussion

Groups with explicitly assigned policies can be filtered using a search string. 

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating groups.
2. Navigate to **Administration Panel / Security / Groups / Index**. 

## Actions/Steps

1. Click the **Edit** button corresponding to a **Role Name** known to have **Assigned Policies** \(e.g. "SYSTEM"\).

![](../../../../../../.gitbook/assets/image%20%28377%29.png)

2. Select the **Search** bar in the top-right corner of the **Assigned Policies** panel.

![](../../../../../../.gitbook/assets/image%20%28363%29.png)

3. Enter a search string for some explicitly **Assigned Policies** \(e.g. "Login"\).

## Expected Behaviour

* The table of **Assigned Policies** should be filtered to show only policies that have names with a substring matching the search string entered. 

![](../../../../../../.gitbook/assets/image%20%28362%29.png)

