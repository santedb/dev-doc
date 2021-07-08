---
description: Testing the successful adding a new security application.
---

# TEST: SECURITY-AA-02

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.add**" command followed by a name you wish to give to the new application \(for instance "Application-Create-Test-11"\).

```text
> application.add Application-Create-Test-11
```

2- To test the  validation of the created application use "**application.list**" command \(This command lists all the Applications \)

```text
> application.list
```

## Expected Behaviour

1- Should show : "Application secret: ..." followed by "CREATE &lt;applican name&gt;".

```text
> application.add Create-Application-Test-11
Application secret: E17BB4F8B41A
CREATE Create-Application-Test-11
>
```

2- Should the newly created Application appear\("Create-Application-Test-11"\) on the list of applications.

```text
> application.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
4061c8fa-db40-11eb-8249-00155d640b09   Create-Application-Te...                                               0    *        0    *
0408b8ec-c17d-11ea-9f72-00155d640b09   izprog                   2020-07-08T20:47:36...                        0    *
d185e6c0-c158-11ea-9f6f-00155d640b09   OMRS198                  2021-03-02T23:21:36...                        0    *
54558ca5-c093-11ea-9f6f-00155d640b09   fiddler                  2021-06-18T11:06:21...                        0    *
54558d8b-c093-11ea-9f6f-00155d640b09   org.santedb.disconnec...                                               0    *
feeca9f3-805e-4be9-a5c7-30e6e495939b   org.santedb.disconnec... 2020-08-03T16:18:55...                        0    *
b7eca9f3-805e-4be9-a5c7-30e6e495939b   org.santedb.disconnec...                                               0    *
```

