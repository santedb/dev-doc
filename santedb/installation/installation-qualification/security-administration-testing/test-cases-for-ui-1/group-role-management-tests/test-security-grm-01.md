---
description: Testing the attempted creation of a Group with required fields missing.
---

# TEST: SECURITY-GRM-02

## References

* [Group / Role Management](../../../../../operations/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-01](test-security-grm-01-1.md)

## Discussion

Only one group property is specifically required from user input during new group creation and that is the **Name**. This test verifies the required **Name** field has a prompt with a validation message. Note that Group ID is required, but is automatically generated.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating groups.
2. Navigate to **Administration Panel / Security / Groups / Index**. 

## Actions/Steps

1. Click the **Create** button.

![](../../../../../../.gitbook/assets/image%20%28295%29.png)

2. Click the **Save** button.

![](../../../../../../.gitbook/assets/image%20%28337%29.png)

## Expected Behaviour

* No group should be created.
* Remain on **Administration Panel / Security / Groups / Create Group** page.
* Display a prompt below the required **Name** textbox with a validation message as follows:

![](../../../../../../.gitbook/assets/image%20%28296%29.png)

