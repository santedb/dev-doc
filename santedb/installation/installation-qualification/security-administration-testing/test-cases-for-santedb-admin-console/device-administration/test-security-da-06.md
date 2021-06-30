# TEST: SECURITY-DA-06

## References

* [Device Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when undeleting a deleted device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.undel**" command followed by the name of the device you wish to undelete.

```text
> device.undel Create-Device-Test
>
```

2- **Test Validation**: Use "**device.list**" command .\(This command lists all the devices\)

```text
> device.list
```

## Expected Behaviour

1- Should 

```text
> device.undel Create-Device-Test
>
```

2- Should the deleted device  \("Create-Device-Test"\) reappear on the list of devices.

```text
> device.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
d73a8f8c-d361-11eb-8248-00155d640b09   Create-Device-Test       2021-06-22T10:41:38...                        0    *
8a5c2e0c-c096-11ea-9f6f-00155d640b09   OSS-SANTEMPI-EL          2021-06-30T18:28:34...                        0    *
```

