---
description: >-
  Testing the unsuccessful creation of a new device when using duplicate
  records.
---

# TEST: SECURITY-DM-09

## References

* [Device Management](broken-reference)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new device using duplicate records (duplicate Name).



## **Pre-Conditions / Setup**

1. User must be logged into an account with policies granted for creating devices.
2. Navigate to **Administration Panel / Security / Devices / Devices**.

## Actions/Steps

1- Click the **Create** button.

![](<../../../../../../.gitbook/assets/1 (12).jpg>)

2- Fill out all the fields appropriately and for the Name field, use a name with which a device exists. (for example "Create-Device-Test")

## Expected Behaviour

1- Should navigate to the new Create Device page.

![](<../../../../../../.gitbook/assets/2 (6).jpg>)

2- Should show an error message below Name field indicating that duplicate record detected.

![](<../../../../../../.gitbook/assets/5 (3).jpg>)
