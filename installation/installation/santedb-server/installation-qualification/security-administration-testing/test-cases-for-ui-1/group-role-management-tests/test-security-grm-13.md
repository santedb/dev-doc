---
description: >-
  Testing the Search textbox for querying members while editing a group's
  Members.
---

# TEST: SECURITY-GRM-15

## References

* [Group / Role Management](../../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-13](test-security-grm-11.md)

## Discussion

Groups with explicitly assigned members can be filtered using a search string.&#x20;

## Pre-Conditions / Setup

1. Follow the instructions from [TEST: SECURITY-GRM-13](test-security-grm-11.md) to create a group and assign a member.
2. Repeat the actions/steps from [TEST: SECURITY-GRM-13](test-security-grm-11.md) until a few different members have been added and saved.

![](<../../../../../../../.gitbook/assets/image (379).png>)

## Actions/Steps

1\. Select the **Search** bar in the top-right corner of the **Members** panel.

![](<../../../../../../../.gitbook/assets/image (381).png>)

\
2\. Enter a search string for some explicitly assigned **Members** (e.g. "admin").

## Expected Behaviour

* The table of **Members** should be filtered to show only members that have names with a substring matching the search string entered.&#x20;

![](<../../../../../../../.gitbook/assets/image (382).png>)
