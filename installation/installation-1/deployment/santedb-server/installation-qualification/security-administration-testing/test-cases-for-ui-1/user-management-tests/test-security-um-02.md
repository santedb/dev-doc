---
description: Testing attempted creation of a new user with required properties missing.
---

# TEST: SECURITY-UM-02

## References

* [User Management](broken-reference)
* [TEST: SECURITY-UM-01](test-security-um-01.md)

## Discussion

Some user properties are specifically required to successfully create a new user. This test verifies required fields have a prompt with a validation message. Required fields are:

* Username
* Role(s)
* New/Confirm Password
* Given Name(s)

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Create User** by clicking the **Create** button on the **Administration Panel / Security / Users / Index** page.

## Actions/Steps

1\. Click the **Save** button.  &#x20;

![](../../../../../../../../.gitbook/assets/blankcreate\_savebutton.png)

## Expected Behaviour

* No user should be created.
* Remain on **Administration Panel / Security / Users / Create User** page.
* Display a prompt below each required property textbox with a validation message as follows:

![](../../../../../../../../.gitbook/assets/blankcreate\_prompted.png)
