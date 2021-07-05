# TEST: SECURITY-AA-05

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when deleting an existing application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.del**" command followed by the name of the application you wish to delete.

```text
> application.del Create-Application-Test
```

2- **Test Validation**: Use "**application.list**" command .\(This command lists all the applications\)

```text
> application.list
```

## Expected Behaviour

1- Should 

```text
> application.del Create-Application-Test
>
```

2- Should  the deleted appliction \("Create-Application-Test"\)  disappear from the list of applications.

```text
> application.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
ebb1fb1a-d8d1-11eb-8249-00155d640b09   test2                                                                  0    *
e30f0976-d8d1-11eb-8249-00155d640b09   test                                                                   0    *
bc8221bc-9cbd-11eb-be65-00155d640b09   test-new4                                                              0    *
a9ada8ae-9cbd-11eb-be65-00155d640b09   test-new3                                                              0    *
8bd857d4-9cbd-11eb-be65-00155d640b09   test-new2                                                              0    *
5d685f5c-9cbd-11eb-be65-00155d640b09   test-redir-to-new2                                                     0    *
3dd7558a-9cbd-11eb-be65-00155d640b09   test-redir-to-new                                                      0    *
12f3e6a8-9cbd-11eb-be65-00155d640b09   testing-application-2                                                  0    *
f21d70ba-915a-11eb-be65-00155d640b09   testing-application-1                                                  0    *
e5decb04-7e14-11eb-b733-00155d640b09   TEST_HARNESS                                                           0    *
0408b8ec-c17d-11ea-9f72-00155d640b09   izprog                   2020-07-08T20:47:36...                        0    *
d185e6c0-c158-11ea-9f6f-00155d640b09   OMRS198                  2021-03-02T23:21:36...                        0    *
54558ca5-c093-11ea-9f6f-00155d640b09   fiddler                  2021-07-04T15:21:51...                        0    *
54558d8b-c093-11ea-9f6f-00155d640b09   org.santedb.disconnec...                                               0    *
feeca9f3-805e-4be9-a5c7-30e6e495939b   org.santedb.disconnec... 2020-08-03T16:18:55...                        0    *
b7eca9f3-805e-4be9-a5c7-30e6e495939b   org.santedb.disconnec...                                               0    *
54558ccc-c093-11ea-9f6f-00155d640b09   org.santedb.disconnec... 2021-07-04T22:21:47...                        0    *
064c3dbd-8f88-4a5d-a1fa-3c3a542b5e98   org.santedb.administr... 2021-07-04T22:22:23...                        0    *
4c5a581c-a6ee-4267-9231-b0d3d50cc08b   org.santedb.debug        2021-06-22T10:41:45...                        0    *
4c5b9f8d-49f4-4101-9662-4270895224b2   SYSTEM                                                                 0    *
>
```

