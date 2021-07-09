---
description: Testing the successful listing of all locked security devices.
---

# TEST: SECURITY-DA-08

## References

* [Device Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when listing all locked security devices in the SanteDB instance.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.list**" command followed by "**-l**"  parameter.

```text
> device.list -l
```

## Expected Behaviour

 1- Should display the list of all "locked" security devices in the SanteDB instance .

### _**This page needs to update after the bug issue is resolved.**_

