---
description: Testing the user.list command with the optional -l flag specified.
---

# TEST: SECURITY-UA-07

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.list` command is for listing users.&#x20;

* The `-l` parameter is used to filter users and show only **locked** users.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2.

## Actions/Steps

1\. Execute the `user.list` command with the `-l` flag.

```
user.list -l
```

## Expected Behaviour
