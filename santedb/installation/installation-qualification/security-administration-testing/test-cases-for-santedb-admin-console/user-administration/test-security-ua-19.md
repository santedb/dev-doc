---
description: >-
  Testing the user.del command with existing and undeleted username provided as
  -u parameter.
---

# TEST: SECURITY-UA-19

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)
* [TEST: SECURITY-UA-27](test-security-ua-27.md)

## Discussion

The `user.del` command is for de-activating users \(effectively deleting the user\) and has a single `-u` parameter for specifying **username** of user to delete. 

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.
3. See [TEST: SECURITY-UA-27](test-security-ua-27.md) for checking if a user is active \(un-deleted\).

## Actions/Steps

1. Execute the `user.del` command with `-u` parameter specified as an existing and active username.

```text
user.del -u demoadmin
```

## Expected Behaviour

* Admin Console output should appear as follows:

```text
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

