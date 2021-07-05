# TEST: SECURITY-DM-05

## References

* [Device Management](../../../../../operations/security-administration/device-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when undeleting  a deleted device.

## Pre-Conditions / Setup

A user should have been logged in and have the right to undelete a device.

## Actions/Steps

1- Navigate to the Devices/Devices page and click the **Show Deleted** button.

![](../../../../../../.gitbook/assets/14%20%282%29.jpg)

2- Click the **Un-Delete** button to undelete the device.

![](../../../../../../.gitbook/assets/15-1.jpg)

3- Click  **Ok** to confirm the undelete.

![](../../../../../../.gitbook/assets/16-1%20%281%29.jpg)

## Expected Behaviour

1- Deleted device \( Create-Device-Test1 \) should appear among the deleted applications.

![](../../../../../../.gitbook/assets/15%20%283%29.jpg)

2- Should display a message asking to confirm the undelete.

![](../../../../../../.gitbook/assets/16%20%282%29.jpg)

3-

* The undeleted device \(Create-Device-Test1 \) should disappear from the deleted devices list page 
* The undeleted device \(Create-Device-Test1\) should reappear on the Devices/Devices page.

![](../../../../../../.gitbook/assets/17%20%282%29.jpg)
