---
description: >-
  Testing the user.add command with all required parameters (-r, -u, -p)
  specified and invalid password.
---

# TEST: SECURITY-UA-13

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
