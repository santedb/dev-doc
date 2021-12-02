---
description: >-
  Testing the user.add command with all required parameters (-r, -u, -p)
  specified, but with an existing username.
---

# TEST: SECURITY-UA-12

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.add` command is for adding new users and has 3 required parameters that must pass validation: **role**, **username**, **password**.&#x20;

* The `-r` parameter is used to specify a **role** to assign to the user being newly added.&#x20;
* The `-u` parameter is used to specify a unique **username** to assign to the user being newly added.&#x20;
* The `-p`  parameter is used to specify a **password** that must pass strength validation.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role exists.
3. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username does not exist.

## Actions/Steps

1. Execute the `user.add` command with `-r` parameter specified as an existing role and `-u` parameter specified as an existing username.

```
user.add -r <existing role> -u <existing user>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.add -r USERS -u demoadmin
E:System.Net.WebException: The remote server returned an error: (422) Unprocessable Entity.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (422) Unprocessable Entity.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error Password failed validation
        2:The remote server returned an error: (422) Unprocessable Entity.
```
