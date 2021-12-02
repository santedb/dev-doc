---
description: >-
  Testing the New/Confirm Password textboxes for invalid matching passwords from
  Security Properties.
---

# TEST: SECURITY-UM-09

## References

* [User Management](broken-reference)

## Discussion

Password strength is determined by use of:

* Both uppercase and lowercase alphabetical characters.
* Symbols.
* Numbers.
* More than 10 characters.

As more of each of the items listed above are used, the password is stronger. **Very Weak**, **Weak**, and **Moderate** password strengths are not valid.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Enter either "Clinic@l" for a **Moderate** password or "Clinic" for a **Weak** password or "Clini" for a **Very Weak** password into both **New Password** and **Confirm Password** textboxes.

## Expected Behaviour

* A status bar should be displayed yellow or red or not at all.
* Status bar is labelled to the right of the status bar as either **Moderate** (using "Clinic@l"; shown below) or **Weak** (using "Clinic") or **Very Weak** (using "Clini").

![](<../../../../../../../.gitbook/assets/image (236).png>)

* When all other required fields are provided, clicking **Save** should prompt a **Business Rules Violation** modal with a message stating "password failed validation".

![](<../../../../../../../.gitbook/assets/image (238).png>)
