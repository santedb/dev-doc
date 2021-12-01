---
description: Testing the successful locking a security device.
---

# TEST: SECURITY-DA-03

## References

* [Device Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when locking an existing device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.lock**" command with a "**-l**" flag, followed by the name of the device you wish to lock.

```
> device.lock -l Create-Device-Test
```

2- **Test Validation**: Use "**device.info**" command  followed by device name.

```
> device.info Create-Device-Test
```



## Expected Behaviour

1- Should&#x20;

```
> device.lock -l Create-Device-Test
>
```

2- Should appear  "Lockout" row with some value.

```
> device.info Create-Device-Test
Name: Create-Device-Test
SID: d73a8f8c-d361-11eb-8248-00155d640b09
Invalid Auth: 0
Lockout: 9999-12-21T18:59:59.9999990-05:00
Last Auth: 2021-06-22T10:41:38.7150000-04:00
Created: 2021-06-22T09:57:54.1080000-04:00 (demoadmin)
Updated: 2021-06-30T18:23:41.3412590-04:00 (Administrator)
        Effective Policies:
```
