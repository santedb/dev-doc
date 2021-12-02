---
description: >-
  Testing the user.list command with the optional -u parameter specified such
  that a user is found successfully.
---

# TEST: SECURITY-UA-02

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.list` command is for listing users.&#x20;

* The `-u` parameter is used to specify a **username** to filter the list with.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. A user must be created for a username to be tested as a `-u` parameter (e.g. "demoadmin").

## Actions/Steps

1\. Execute the `user.list` command and specify `demoadmin` **** for the `-u` parameter.

```
user.list -u demoadmin
```

## Expected Behaviour

* The Admin Console output should appear similarly to the following:

```
> user.list -u demoadmin
SID                                    Name                     Last Auth              Lockout                ILA  A
2a348c6e-c158-11ea-9f6f-00155d640b09   demoadmin                2021-07-09T08:30:59...                        0    *
```

