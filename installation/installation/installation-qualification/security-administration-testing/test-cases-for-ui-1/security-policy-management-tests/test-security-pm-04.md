---
description: >-
  Testing the unsuccessful creation of a new policy when using duplicate
  records.
---

# TEST: SECURITY-PM-04

## References

* [Security Policy Management](../../../../../../operations-1/system-administration/security-administration/security-policy-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new policy using duplicate records (duplicate OID and/or duplicate Name)



## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating policies.
2. Navigate to **Administration Panel / Security / Policies / Index**.

## Actions/Steps

1- Click the **Create** button.

![](<../../../../../../.gitbook/assets/1 (10).jpg>)

2- Fill out all the fields appropriately and for the Name field, use a name with which a policy exists. (for example "Create-Policy-Test").

3- For the OID filed, use an OID with which a policy exists. (for example "1.3.6.1.4.1.3349.3.1.5.9.2.99.2").





## Expected Behaviour

1- Should navigate to the new Create Policy page.

![](<../../../../../../.gitbook/assets/dnld1 (2).jpg>)

2- Should show an error message below Name field indicating that duplicate record detected.

![](<../../../../../../.gitbook/assets/5 (2).jpg>)

3- Should show an error message below OID field indicating that duplicate record detected.

![](<../../../../../../.gitbook/assets/6 (3).jpg>)
