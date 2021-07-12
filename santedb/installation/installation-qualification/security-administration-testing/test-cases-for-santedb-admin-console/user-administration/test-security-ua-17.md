---
description: Testing the user.del command with no parameters specified.
---

# TEST: SECURITY-UA-17

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.` command is for &lt;&gt; and the `-` parameter is used to &lt;&gt;.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A user must be created and have status changed to non-active \(i.e. delete the user\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `user.` command with the `-` parameter specified as '&lt;&gt;'.

```text
user. -
```

## Expected Behaviour

