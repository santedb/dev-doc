---
description: Testing the Employer textbox from Demographic Properties with multiple values.
---

# TEST: SECURITY-UM-19

## References

* [User Management](../../../../../../operations/system-administration/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-16](test-security-um-16.md)

## Discussion

New users being created can be assigned multiple employers in the **Employer** textbox.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Follow the same actions/steps from [TEST: SECURITY-UM-16](test-security-um-16.md), but use the **Employer** textbox and a corresponding valid listed values (e.g. "Elbonia National Health Insurnace Programme" and "Dilbert Vaccine Manufacturers") instead of the **Primary Facility** textbox and a corresponding multiple values (e.g. "ELBONIA" and "Good Health Hospital").

## Expected Behaviour

* Multiple tags appear, each representing an **Employer** for a new user being created and can be removed from the **Employer** textbox.

![](<../../../../../../.gitbook/assets/image (279).png>)
