---
description: >-
  Testing the unsuccessful creation of a new device when device name parameter
  missing
---

# TEST: SECURITY-DA-13

## References

* [Device Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security device **** without specifying the device name parameter.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.add**" command.

```
> device.add
```

## Expected Behaviour

1- Should show : "Device secret: ..." followed by an Error message indicating that name can not be null.

```
> device.add
Device secret: 178DAC6DE7CDDA44A789B57D5606A7AD
ERR: Exception has been thrown by the target of an invocation.
        1:Value cannot be null.
Parameter name: source
>
```
