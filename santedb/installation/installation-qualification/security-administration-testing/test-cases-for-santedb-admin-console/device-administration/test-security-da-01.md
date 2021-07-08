---
description: Testing the successful adding a new security device.
---

# TEST: SECURITY-DA-02

## References

* [Device Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**device.add**" command followed by a name you wish to give to the new device \(for instance "Device-Create-Test-11"\).

```text
> device.add Device-Create-Test-11
```

2- To test the  validation of the created device use "**device.list**" command \(This command lists all the devices \)

```text
> device.list
```

## Expected Behaviour

1- Should show : "Device Secret: ..." followed by "CREATE &lt;device name&gt;".

```text
> device.add Create-Device-Test-11
Device secret: 24E31E11CE70C941855A62080C12EC53
CREATE Create-Device-Test-11
>
```

2- Should the newly created device appear\("Create-Device-Test-11"\) on the list of devices.

```text
> device.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
8a5c2e0c-c096-11ea-9f6f-00155d640b09   OSS-SANTEMPI-EL          2021-06-30T10:59:44...                        0    *
c509891a-d9b2-11eb-8249-00155d640b09   Create-Device-Test-11                                                  0    *
```

