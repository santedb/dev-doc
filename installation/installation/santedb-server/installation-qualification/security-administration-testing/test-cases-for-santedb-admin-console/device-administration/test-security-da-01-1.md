---
description: Testing the successful listing of all security devices.
---

# TEST: SECURITY-DA-01

## References

* [Device Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when listing security devices.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.list**" command.

```
> device.list
```

## Expected Behaviour

1- Should display the list of all security devices in the SanteDB instance .

```
> device.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
8a5c2e0c-c096-11ea-9f6f-00155d640b09   OSS-SANTEMPI-EL          2021-07-02T09:19:23...                        0    *
d73a8f8c-d361-11eb-8248-00155d640b09   Create-Device-Test       2021-06-22T10:41:38...                        0    *
f956bd56-d9a2-11eb-8249-00155d640b09   help                                                                   0    *
b1006a6c-d514-11eb-8248-00155d640b09   testDevice                                                             0    *
55bece52-d422-11eb-8248-00155d640b09   ETSTST                                                                 0    *
959617ca-d2af-11eb-8248-00155d640b09   Debugee-0060739CE9C9     2021-06-22T09:27:35...                        0    *
a51d8dd4-c2f3-11eb-8247-00155d640b09   Debugee-00607347B3D3     2021-06-22T09:21:22...                        0    *
```
