# TEST: SECURITY-DA-05

## References

* [Device Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when deleting an existing device.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.del**" command followed by the name of the device you wish to delete.

```text
> device.del Create-Device-Test
```

2- **Test Validation**: Use "**device.list**" command .\(This command lists all the devices\)

```text
> device.list
```

## Expected Behaviour

1- Should 

```text
> device.del Create-Device-Test
>
```

2- Should disappear the deleted device \("Create-Device-Test"\) from the list of devices.

```text
> device.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
8a5c2e0c-c096-11ea-9f6f-00155d640b09   OSS-SANTEMPI-EL          2021-06-30T14:52:44...                        0    *
f956bd56-d9a2-11eb-8249-00155d640b09   help                                                                   0    *
b1006a6c-d514-11eb-8248-00155d640b09   testDevice                                                             0    *
55bece52-d422-11eb-8248-00155d640b09   ETSTST                                                                 0    *
959617ca-d2af-11eb-8248-00155d640b09   Debugee-0060739CE9C9     2021-06-22T09:27:35...                        0    *
a51d8dd4-c2f3-11eb-8247-00155d640b09   Debugee-00607347B3D3     2021-06-22T09:21:22...                        0    *
4f772c96-d2c5-11eb-8248-00155d640b09   test_Tommy               2021-06-22T09:21:07...                        0    *
b82d6a04-b1ad-11eb-be66-00155d640b09   Debugee-0050569D1665     2021-06-21T12:05:43...                        0    *
b61bc8b6-6c64-11eb-ba3b-00155d640b09   Debugee-E0D55EA5D6CD     2021-06-18T11:34:03...                        0    *
cb44189a-cd41-11eb-8247-00155d640b09   newversion               2021-06-14T14:58:14...                        0    *
8957d69c-cd41-11eb-8247-00155d640b09   test-debuggee            2021-06-14T14:51:58...                        0    *
d7071440-c47f-11eb-8247-00155d640b09   medic-tom-009            2021-06-03T15:45:06...                        0    *
5ac0b2aa-b1ca-11eb-be66-00155d640b09   Debugee-0050569D809D     2021-06-03T14:36:13...                        0    *
7e02f484-c47c-11eb-8247-00155d640b09   tom-medic-003            2021-06-03T11:01:36...                        0    *
0211a59a-be3d-11eb-8246-00155d640b09   medic-tom-11             2021-06-02T14:13:46...                        0    *
7e4a2a36-be30-11eb-8246-00155d640b09   medic-tom-1              2021-05-26T11:37:09...                        1    *
f8153a48-b4be-11eb-8246-00155d640b09   medic-tom-007            2021-05-14T10:31:34...                        0    *
bb33ce7a-a77e-11eb-be66-00155d640b09   medic-007-Debugee-0A0... 2021-05-13T22:24:18...                        0    *
aafa2c8c-658b-11eb-a81a-00155d640b09   Debugee-00155D646402     2021-04-13T21:12:23...                        0    *
b145b214-9641-11eb-be65-00155d640b09   FOO                                                                    0    *
1bbad350-90f6-11eb-be65-00155d640b09   medic-Debugee-0A00270... 2021-04-09T16:56:03... 2021-04-27T02:36:09... 77   *
9965f35c-9641-11eb-be65-00155d640b09   EXT43                                                                  0    *
6de5add0-9641-11eb-be65-00155d640b09   EXT                                                                    0    *
f67c4060-9640-11eb-be65-00155d640b09   NEWDEV                                                                 0    *
d2d60d80-9640-11eb-be65-00155d640b09   TESTCREATE                                                             0    *
6d31ab38-90fa-11eb-be65-00155d640b09   the-ultimate-testier                                                   0    *
eee4d784-7e14-11eb-b733-00155d640b09   TEST|TEST_HARNESS                                                      0    *
a8333b2c-7c5d-11eb-b733-00155d640b09   Debugee-0A0027000007-... 2021-03-28T21:12:24...                        160  *
79da4440-8e74-11eb-be65-00155d640b09   boaty-mcboatface                                                       0    *
d7fd2d76-672e-11eb-a81f-00155d640b09   Debugee-0A0027000007     2021-03-03T15:12:31...                        0    *
fc2c008a-c158-11ea-9f6f-00155d640b09   OMRS198|CLINIC_B         2021-03-02T23:21:36...                        0    *
af41577d-6a3f-11eb-b9c4-00155d640b09   Debugee-A44CC810DE2E     2021-02-22T14:23:06...                        0    *
b13850aa-6c76-11eb-ba3b-00155d640b09   MOTHERSHIP               2021-02-15T01:56:00...                        0    *
a4bd5376-1595-11eb-8208-00155d640b09   Debugee-482AE32B88DD     2021-02-08T13:17:28...                        0    *
f4fc1572-69fd-11eb-aa93-00155d640b09   Debugee-D481D75B7BD3     2021-02-08T06:11:03...                        0    *
2db80602-678b-11eb-a866-00155d640b09   Debugee-2C4D545878CA     2021-02-05T07:03:53...                        0    *
02abb15a-6792-11eb-a86a-00155d640b09   Debugee-2C4D545878CB     2021-02-05T04:47:35...                        0    *
a056c0e8-672b-11eb-a81f-00155d640b09   Debugee-0A0027000007-... 2021-02-04T16:16:49...                        0    *
e2da5c56-c15f-11ea-9f70-00155d640b09   OSS-SANTEMPI-DC          2020-08-03T16:17:28...                        0    *
```

