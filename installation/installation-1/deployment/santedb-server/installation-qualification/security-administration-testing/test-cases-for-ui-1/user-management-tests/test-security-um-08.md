---
description: >-
  Testing the New/Confirm Password textboxes for valid matching passwords from
  Security Properties.
---

# TEST: SECURITY-UM-08

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

Password strength is determined by use of:

* Both uppercase and lowercase alphabetical characters.
* Symbols.
* Numbers.
* More than 10 characters.

As more of each of the items listed above are used, the password is stronger. **Strong** and **Very Strong** passwords are valid.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Enter either "Clinic@l12" for a **Strong** password or "Clinic@l123" for a **Very Strong** password into both **New Password** and **Confirm Password** textboxes.

## Expected Behaviour

* A status bar should be displayed green and labelled to the right of the status bar as either **Strong** (using "Clinic@l12"; shown below) or **Very Strong** (using "Clinic@l123").
* A new user can successfully be created after entering remaining required fields (see [TEST: SECURITY-UM-01](test-security-um-01.md)).

![](<../../../../../../../../.gitbook/assets/image (231).png>)
