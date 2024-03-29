---
description: Testing the successful deleting a device.
---

# TEST: SECURITY-DM-04

## References

* [Device Management](../../../../../../../operations-1/system-administration/security-administration/device-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when deleting an existing device.

## **Pre-Conditions / Setup**

1. User must be logged into an account with policies granted for deleting devices.
2. Navigate to **Administration Panel / Security / Devices / Devices**.

## Actions/Steps

1- Click the **Delete** button.

![](<../../../../../../../.gitbook/assets/11 (1).jpg>)

2- Click  **Ok** to confirm the delete.

![](../../../../../../../.gitbook/assets/12-1.jpg)

## Expected Behaviour

1- Should display a message asking to confirm the delete.

![](<../../../../../../../.gitbook/assets/12 (2).jpg>)

2- Deleted device (Create-Device -Test1) Should disappear from the Devices/Devices page.

![](<../../../../../../../.gitbook/assets/13 (2).jpg>)
