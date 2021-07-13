---
description: Testing the user.del command with no parameters specified.
---

# TEST: SECURITY-UA-17

## References

* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)

## Discussion

The `user.del` command is for de-activating users \(effectively deleting the user\) and has a single `-u` parameter for specifying **username** of user to delete. 

* An exception is thrown when no username is specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `user.del` command.

```text
user.del
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

