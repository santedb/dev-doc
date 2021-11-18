---
description: Testing the successful adding a new security device and setting device secret.
---

# TEST: SECURITY-DA-10

## References

* [Device Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security device and setting device secret.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.add**" command followed by a name you wish to give to the new device (for instance "Create-Device-SDBAC4") followed by  "**-s**" parameter followed by the secret you want to set.

```
> devdevice.add Create-Device-SDBAC4 -s TestSecret
```

## Expected Behaviour

1- Should show : "CREATE \<device name>".&#x20;

{% hint style="info" %}
In this case the Device Secret is not displayed as usually it is after creating a device since the secret is what we have set after "-s" parameter.
{% endhint %}

```
> device.add Create-Device-SDBAC4 -s TestSecret
CREATE Create-Device-SDBAC4
>
```
