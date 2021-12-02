---
description: Testing the role.add command with no parameters specified.
---

# TEST: SECURITY-GRA-06

## References

* [Group / Role Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**.&#x20;

* An exception should be thrown when no parameters are specified.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1. Execute the `role.add` command.

```
role.add
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> role.add
E:System.Net.WebException: The remote server returned an error: (422) Unprocessable Entity.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (422) Unprocessable Entity.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error 23502: null value in column "rol_name" violates not-null constraint
        2:The remote server returned an error: (422) Unprocessable Entity.
```
