---
description: >-
  Testing the user.password command with existing username provided as -u
  parameter and with invalid password provided as -p parameter.
---

# TEST: SECURITY-UA-34

## References

* [User Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.password` command is for changing a specific users password.&#x20;

* The `-u` parameter is used to specify the **username **of which user's password to change.&#x20;
* The `-p`  parameter is used to specify a **password **that must pass strength validation.
* An exception is thrown when an invalid (weak) password is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.

## Actions/Steps

1\. Execute the `user.password` command with `-u` parameter specified as an existing username and `-p` parameter specified as a weak password.

```
user.password -u <existing username> -p NotSecure
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.password -u demoadmin -p NotSecure
E:System.Net.WebException: The remote server returned an error: (422) Unprocessable Entity.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (422) Unprocessable Entity.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error Password does not meet complexity requirements
        2:The remote server returned an error: (422) Unprocessable Entity.
```
