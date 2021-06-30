# TEST: SECURITY-DA-02

## References

* [Device Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Type in "**device.add**" command followed by a name you wish to give to the new device \(for instance "Device-Create-Test-11"\).

```text
> device.add Device-Create-Test-11
```

## Expected Behaviour

1- Should appear a "Device Secret" followed by "CREATE &lt;device name&gt;".

```text
> device.add Create-Device-Test-11
Device secret: 24E31E11CE70C941855A62080C12EC53
CREATE Create-Device-Test-11
>
```



