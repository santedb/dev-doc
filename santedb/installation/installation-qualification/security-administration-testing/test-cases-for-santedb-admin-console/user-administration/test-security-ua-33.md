---
description: >-
  Testing the user.password command with non-existing username provided as -u
  parameter only.
---

# TEST: SECURITY-UA-33

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.password` command is for changing a specific users password. 

* The `-u` parameter is used to specify the username of the user who's password will change. 
* An exception is thrown when the username specified does not exist. 

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. A user must be created and have status changed to non-active \(i.e. delete the user\) for testing the `-` flag to show the non-active user.

## Actions/Steps

1. Execute the `user.` command with the `-` parameter specified as '&lt;&gt;'.

```text
user.password -u <new user name>
```

## Expected Behaviour

