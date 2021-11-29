# Device Administration

You can use the iCDR administrative console to create, list, lock, unlock and get information about devices within the iCDR instance. Changing a device secret needs to be done through the UI. For more information visit 'Changing Device Secret' section of  [Device Management](../../security-administration/device-management.md).&#x20;

## Viewing Devices

You can view devices in the system using the `device.list` command, specifying optional filter paramters.

```
> device.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
8a5c2e0c-c096-11ea-9f6f-00155d640b09   OSS-SANTEMPI-EL          2021-06-29T23:15:44...                        0    *
6552ba82-d8fe-11eb-8249-00155d640b09   Create-Device-Test-0                                                   0    *
d73a8f8c-d361-11eb-8248-00155d640b09   Create-Device-Test       2021-06-22T10:41:38... 9999-12-21T18:59:59... 0    *
b1006a6c-d514-11eb-8248-00155d640b09   testDevice                                                             0    *
55bece52-d422-11eb-8248-00155d640b09   ETSTST                                                                 0    *
959617ca-d2af-11eb-8248-00155d640b09   Debugee-0060739CE9C9     2021-06-22T09:27:35...                        0    *
```

The optional filter parameters for `device.list` **** are:

| Parameter | Description                | Example          |
| --------- | -------------------------- | ---------------- |
| `-l`      | Filter on locked status    | `device.list -l` |
| `-a`      | Include non-active devices | `device.list -a` |

## Adding Devices

You can add a device to the iCDR instance using the `device.add` command and specifying the name you wish to give to the device:

```
> device.add Create-Device-Test-10
Device secret: AFF89DA48479B8478748BD11A9BD8F20
CREATE Create-Device-Test-10
>
```

The parameters for `device.add` are:

| Parameter | Description                      | Example                                                       |
| --------- | -------------------------------- | ------------------------------------------------------------- |
| `-s`      | The device secret to set         | `device.add <device_name> -s s3CreT`                          |
| `-g`      | The policies to grant the device | `device.add <device_name> -g 1.3.6.1.4.1.33349.3.1.5.9.2.999` |
| `-d`      | The policies to deny the device  | `device.add <device_name> -d 1.3.6.1.4.1.33349.3.1.5.9.2.999` |

## Locking/Unlocking Devices

To lock or unlock a device, the `device.lock` command with our without the `-l` flag to specify whether the lock should be set or unset.

To lock the device "Create-Device-Test":

```
> device.lock -l Create-Device-Test
```

To unlock the device "Create-Device-Test":

```
> device.lock Create-Device-Test
```

## Deleting/Undeleting Devices

To delete a device, the **`device.del`** command is used specifiying the device name.

To delete the device "Create-Device-Test":

```
> device.del Create-Device-Test
```

To undelete a device, the `device.undel` command is used specifying the device name.

To undelete the device "Create-Device-Test":

```
> device.undel Create-Device-Test
```

## Assigning Policies to a Device

To assign a policy to a device please visit 'Assigning Policies' section of [Policy Administration](policy-administration.md).

## Device Info View

You can get extended information about a particular device by using the `device.info` command and specifying the device name. For example, to get information about the device Create-Device-Test:

```
> device.info Create-Device-Test
Name: Create-Device-Test
SID: d73a8f8c-d361-11eb-8248-00155d640b09
Invalid Auth: 0
Lockout:
Last Auth: 2021-06-22T10:41:38.7150000-04:00
Created: 2021-06-22T09:57:54.1080000-04:00 (demoadmin)
Updated: 2021-06-30T03:42:25.5389080-04:00 (Administrator)
        Effective Policies:
                Unrestricted All [1.3.6.1.4.1.33349.3.1.5.9.2] : --- (default DENY)
                Unrestricted Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.0] : --- (default DENY)
                Change Password [1.3.6.1.4.1.33349.3.1.5.9.2.0.1] : --- (default DENY)
                Administer Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.0.10] : --- (default DENY)
                Access Audit Log [1.3.6.1.4.1.33349.3.1.5.9.2.0.11] : --- (default DENY)
                Administer Applets [1.3.6.1.4.1.33349.3.1.5.9.2.0.12] : --- (default DENY)
                Assign Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.13] : --- (default DENY)
                Unrestricted PubSub Administration [1.3.6.1.4.1.33349.3.1.5.9.2.0.14] : --- (default DENY)
                Create/Alter PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.1] : --- (default DENY)
                Disable/Enable PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.2] : --- (default DENY)
                Delete PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.3] : --- (default DENY)
                Read PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.4] : --- (default DENY)
                Create Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.2] : --- (default DENY)
                Alter Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.3] : --- (default DENY)
                Create Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.4] : --- (default DENY)
                Create Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1] : Grant (explicit)
                Create Device [1.3.6.1.4.1.33349.3.1.5.9.2.0.5] : --- (default DENY)
                Create Application [1.3.6.1.4.1.33349.3.1.5.9.2.0.6] : --- (default DENY)
                Administer Concept Dictionary [1.3.6.1.4.1.33349.3.1.5.9.2.0.7] : --- (default DENY)
                Alter Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.8] : --- (default DENY)
                Alter Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1] : --- (default DENY)
                Alter Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.9] : --- (default DENY)
                Login [1.3.6.1.4.1.33349.3.1.5.9.2.1] : --- (default DENY)
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : Grant (explicit)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : Grant (inherited from Login as a Service)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : --- (default DENY)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : --- (default DENY)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : --- (default DENY)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : --- (default DENY)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : Grant (inherited from Login as a Service)
                Allow Impersonation of Application [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2] : Grant (inherited from Login as a Service)
                Access Client Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.10] : --- (default DENY)
                Unrestricted Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2] : Grant (explicit)
                Query Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.0] : Grant (inherited from Unrestricted Clinical Data)
                Write Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.1] : Grant (inherited from Unrestricted Clinical Data)
                Delete Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.2] : Grant (inherited from Unrestricted Clinical Data)
                Read Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.3] : Grant (inherited from Unrestricted Clinical Data)
                Export Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.4] : Grant (inherited from Unrestricted Clinical Data)
                Elevate Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.5] : Grant (inherited from Unrestricted Clinical Data)
                Unrestricted Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4] : Grant (explicit)
                Read Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4.0] : Grant (explicit)
                Read Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2] : Grant (inherited from Read Metadata)
                Query Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3] : Grant (inherited from Read Metadata)
                Read Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2] : Grant (inherited from Read Metadata)
                Query Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3] : Grant (inherited from Read Metadata)
                Write Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0] : Grant (inherited from Unrestricted Metadata)
                Delete Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1] : Grant (inherited from Unrestricted Metadata)
                Write Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0] : Grant (inherited from Unrestricted Metadata)
                Delete Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1] : Grant (inherited from Unrestricted Metadata)
                Unrestricted Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.5] : --- (default DENY)
                Write Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.0] : --- (default DENY)
                Delete Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.1] : --- (default DENY)
                Read Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.2] : --- (default DENY)
                Query Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.3] : --- (default DENY)
                Unrestricted MDM [1.3.6.1.4.1.33349.3.1.5.9.2.6] : --- (default DENY)
                Write MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.1] : --- (default DENY)
                Read MDM Locals [1.3.6.1.4.1.33349.3.1.5.9.2.6.2] : --- (default DENY)
                Merge MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.3] : --- (default DENY)
                Special Security Elevation [1.3.6.1.4.1.33349.3.1.5.9.2.600] : Elevate (explicit)
                Change Security Challenge Question [1.3.6.1.4.1.33349.3.1.5.9.2.600.1] : Elevate (inherited from Special Security Elevation)
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Deny (explicit)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
>
```
