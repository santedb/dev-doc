---
description: >-
  Testing the successful adding a new security device with setting the policies
  to grant the device.
---

# TEST: SECURITY-DA-11

## References

* [Device Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security device with setting the policies to grant the device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.add**" command followed by a name you wish to give to the new device (for instance "Create-Device-SDBAC5") followed by  "**-g**" parameter followed by the policy OID you want to grant the device.(for example 1.3.6.1.4.1.33349.3.1.5.9.2.999 (Override Disclosure))

```
> device.add Create-Device-SDBAC5 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999
```

2- To test the  validation of the created device with granted policy use "**device.info**" command  followed by the Device Name (This command displays all the detailed information about a device )

```
> device.info Create-Device-SDBAC5
```

## Expected Behaviour

1-  Should show : "Device secret: ..." followed by "CREATE \<device name>".

```
> device.add Create-Device-SDBAC5 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999
Device secret: F331096BAB32A040A43725D4167F404B
CREATE Create-Device-SDBAC5
>
```

2- Should the assigned policy ("Override Disclosure") appear in the Effective Policies row with action Grant (Explicit)

### _**This page needs to update after the bug issue is resolved.**_
