---
description: >-
  Testing a User Name link to view a device from the Users & Computers section
  within Audit Event Details.
---

# TEST: SECURITY-AR-03

## References

* [Audit Repository](../../../../../../operations/system-administration/security-administration/audit-repository.md)
* [TEST: SECURITY-AR-01](test-security-ar-01.md)

## Discussion

When a device is an actor involved in an audit event, a link can be followed to that user from the **Audit Event Details**.

## Pre-Conditions / Setup

1. User must have permission to view the list of other devices.
2. Follow the instructions from [TEST: SECURITY-AR-01](test-security-ar-01.md) to view the details of some **Audit Event **involving a device.

## Actions/Steps

1\. Click on the **Users & Computers** accordion-panel heading.

![](<../../../../../../.gitbook/assets/image (371).png>)

2\. Click on a device's **User Name **appearing in the list of **Users & Computers **(e.g. "OSS-SANTEMPE-EL").

![](<../../../../../../.gitbook/assets/image (351).png>)

## Expected Behaviour

* Automatically navigate to the **Administration Panel / Security / Devices / Index **page.
* Automatically enter search string to show the device that was clicked.

![](<../../../../../../.gitbook/assets/image (360).png>)
