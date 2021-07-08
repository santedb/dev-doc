---
description: Testing the successful listing of all security applications.
---

# TEST: SECURITY-AA-01

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when listing all security applications in the SanteDB instance.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.list**" command.

```text
> application.list
```

## Expected Behaviour

1- Should display the list of all security applications in the SanteDB instance .

```text
> application.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
eeb716ee-d94c-11eb-8249-00155d640b09   Create-Application-Te...                                               0    *
0408b8ec-c17d-11ea-9f72-00155d640b09   izprog                   2020-07-08T20:47:36...                        0    *
d185e6c0-c158-11ea-9f6f-00155d640b09   OMRS198                  2021-03-02T23:21:36...                        0    *
54558ca5-c093-11ea-9f6f-00155d640b09   fiddler                  2021-06-18T11:06:21...                        0    *
54558d8b-c093-11ea-9f6f-00155d640b09   org.santedb.disconnec...                                               0    *
feeca9f3-805e-4be9-a5c7-30e6e495939b   org.santedb.disconnec... 2020-08-03T16:18:55...                        0    *
b7eca9f3-805e-4be9-a5c7-30e6e495939b   org.santedb.disconnec...                                               0    *
54558ccc-c093-11ea-9f6f-00155d640b09   org.santedb.disconnec... 2021-07-02T09:19:33...                        0    *
064c3dbd-8f88-4a5d-a1fa-3c3a542b5e98   org.santedb.administr... 2021-07-02T09:31:49...                        0    *
4c5a581c-a6ee-4267-9231-b0d3d50cc08b   org.santedb.debug        2021-06-22T10:41:45...                        0    *
4c5b9f8d-49f4-4101-9662-4270895224b2   SYSTEM                                                                 0    *
>
```

