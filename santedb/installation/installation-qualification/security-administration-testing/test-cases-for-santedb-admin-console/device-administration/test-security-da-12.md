---
description: >-
  Testing the successful adding a new security device with setting the policies
  to deny the device.
---

# TEST: SECURITY-DA-12

## References

* [Device Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security device and setting the policies to deny the device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.add**" command followed by a name you wish to give to the new device \(for instance "Create-Device-SDBAC6"\) followed by  "**-d**" parameter followed by the policy OID you want to deny the device \(for example 1.3.6.1.4.1.33349.3.1.5.9.2.999 \(Override Disclosure\)\).

```text
> device.add Create-Device-SDBAC7 -d 1.3.6.1.4.1.33349.3.1.5.9.2.999
```

2- To test the  validation of the created device with denied policy use "**device.info**" command  followed by the Device Name \(This command displays all the detailed information about a device \)

```text
 device.info Create-Device-SDBAC7
```

## Expected Behaviour

1-  Should show : "Device secret: ..." followed by "CREATE &lt;device name&gt;".

```text
> device.add Create-Device-SDBAC7 -d 1.3.6.1.4.1.33349.3.1.5.9.2.999
Device secret: 394767092C161043822A32216A5788F5
CREATE Create-Device-SDBAC7
>
```

2- Should the assigned policy \("Override Disclosure"\) appear in the Effective Policies row with action Deny \(Explicit\)

### _**This page needs to update after the bug issue is resolved.**_

