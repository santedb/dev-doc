---
description: >-
  Testing the user.list command with the optional -u parameter specified such
  that a user is not found successfully (does not exist).
---

# TEST: SECURITY-UA-03

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-01](test-security-ua-01.md)

## Discussion

The `user.list` command is for listing users.

* The `-u` parameter is used to specify a **username**.&#x20;
* An exception is thrown when a non-existing username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. A user must be created for a username to be tested as a `-u` parameter (e.g. assume "NOT\_A\_USER" has not been created yet for this test or refer to [TEST: SECURITY-UA-01](test-security-ua-01.md) to find out what usernames are still available).

## Actions/Steps

1\. Execute the `user.list` command and specify `NOT_A_USER` **** for the `-u` parameter.

```
user.list -u NOT_A_USER
```

## Expected Behaviour

* The Admin Console output should appear similarly to the following:

```
> user.list -u NOT_A_USER
E:System.Net.WebException: The remote server returned an error: (403) Forbidden.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (403) Forbidden.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (403) Forbidden.
                REMOTE: Session expired
        2:The remote server returned an error: (403) Forbidden.
```
