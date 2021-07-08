---
description: >-
  Testing the Primary Facility textbox from Demographic Properties with multiple
  values.
---

# TEST: SECURITY-UM-16

## References

* [User Management](../../../../../operations/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

New users being created can be assigned multiple primary facilities in the **Primary Facility** textbox.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1. Select the **Primary Facility** textbox within the **Demographic Properties** section.

![](../../../../../../.gitbook/assets/image%20%28243%29.png)

2. Select an existing **Primary Facility** listed in the dropdown \(e.g. "ELBONIA" is used in this test\).

![](../../../../../../.gitbook/assets/image%20%28255%29.png)

2. Select another existing **Primary Facility** listed in the dropdown \(e.g. "Good Health Hospital" is used in this test\).

## Expected Behaviour

* Multiple tags appear, each representing a **Primary Facility** for a new user being created and can be removed from the **Primary Facility** textbox.

![](../../../../../../.gitbook/assets/image%20%28273%29.png)

