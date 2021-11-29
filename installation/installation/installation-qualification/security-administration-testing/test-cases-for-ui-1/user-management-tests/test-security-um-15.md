---
description: >-
  Testing the Primary Facility textbox from Demographic Properties with an
  invalid value.
---

# TEST: SECURITY-UM-15

## References

* [User Management](../../../../../../operations/system-administration/security-administration/user-management.md)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

While creating new users, any **Primary Facility** being added to a new user's profile must be one that exists as an option from the static list of all primary facilities.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Select the **Primary Facility** textbox within the **Demographic Properties** section.

![](<../../../../../../.gitbook/assets/image (243).png>)

2\. Enter a string value that does not match any existing **Primary Facility** from the dropdown.

## Expected Behaviour

* The dropdown of possible existing primary facilities should only have a single disabled option that simply prompts users: "No results found".

![](<../../../../../../.gitbook/assets/image (246).png>)
