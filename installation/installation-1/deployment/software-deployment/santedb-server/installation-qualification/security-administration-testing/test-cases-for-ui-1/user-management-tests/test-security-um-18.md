---
description: >-
  Testing the Employer textbox from Demographic Properties with an invalid
  value.
---

# TEST: SECURITY-UM-18

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)
* [TEST: SECURITY-UM-15](test-security-um-15.md)

## Discussion

While creating new users, any Employer being added to a new user's profile must be one that exists as an option from the static list of all employers.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Follow the same actions/steps from [TEST: SECURITY-UM-15](test-security-um-15.md), but use the **Employer** textbox and a corresponding invalid value (e.g. "NOT\_AN\_EMPLOYER") instead of the **Primary Facility** textbox and a corresponding invalid value.  &#x20;

## Expected Behaviour

* The dropdown of possible existing employers should only have a single disabled option that simply prompts users: "No results found".

![](<../../../../../../../../../.gitbook/assets/image (262).png>)
