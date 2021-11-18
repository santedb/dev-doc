---
description: Testing the successful unlocking a locked security device.
---

# TEST: SECURITY-DA-04

## References

* [Device Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when unlocking a locked device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.lock**" command followed by the name of the device you wish to unlock.

```
> device.lock Create-Device-Test
```

2- **Test Validation**: Use "**device.info**" command  followed by device name.

```
> device.info Create-Device-Test
```

## Expected Behaviour

1- Should&#x20;

```
> device.lock Create-Device-Test
>
```

2- Should appear the "Lockout" row with no value.

```
> device.info Create-Device-Test
Name: Create-Device-Test
SID: d73a8f8c-d361-11eb-8248-00155d640b09
Invalid Auth: 0
Lockout:
Last Auth: 2021-06-22T10:41:38.7150000-04:00
Created: 2021-06-22T09:57:54.1080000-04:00 (demoadmin)
Updated: 2021-06-30T18:45:45.4109630-04:00 (Administrator)
        Effective Policies:
```
