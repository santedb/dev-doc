---
description: >-
  Testing the unsuccessful creation of a new policy when OID format is
  incorrect.
---

# TEST: SECURITY-PM-03

## References

* [Security Policy Management](../../../../../operations/security-administration/security-policy-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new policy using invalid OID format.



## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating policies.
2. Navigate to **Administration Panel / Security / Policies / Index**.

## Actions/Steps

1- Click the **Create** button

![](../../../../../../.gitbook/assets/1%20%2810%29.jpg)

2- Fill out all the fields appropriately and use the incorrect format for OID field and click the **Save** button.

![](../../../../../../.gitbook/assets/3%20%2815%29.jpg)

## Expected Behaviour

1- Should navigate to the new Create Policy page.

![](../../../../../../.gitbook/assets/dnld1%20%281%29.jpg)

2- Should show an error message below OID field indicating that OID format is invalid.

![](../../../../../../.gitbook/assets/4%20%286%29.jpg)

