---
description: >-
  Testing the unsuccessful creation of a new device when Name, Model Name and
  Operating System fields are missing.
---

# TEST: SECURITY-DM-08

## References

* [Device Management](../../../../../operations/security-administration/device-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new device leaving the Name, Model Name and Operating System fields blank.



## **Pre-Conditions / Setup**

1. User must be logged into an account with policies granted for creating devices.
2. Navigate to **Administration Panel / Security / Devices / Devices**.

## Actions/Steps

1- Click the **Create** button.

![](../../../../../../.gitbook/assets/1%20%288%29.jpg)

2- Leave Name, Model Name and Operating System fields blank and click the **Save** button.\( Name, Model Name and Operating System fields are required fields \) 

![](../../../../../../.gitbook/assets/3%20%2813%29.jpg)

## Expected Behaviour

1- Should navigate to the new Create Device page.

![](../../../../../../.gitbook/assets/2%20%284%29.jpg)

2- Should show an error message below Name field, Model Name field and Operating System field indicating that required field is missing.

![](../../../../../../.gitbook/assets/4%20%285%29.jpg)

