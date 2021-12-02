---
description: >-
  Testing the unsuccessful creation of a new application when application name
  parameter is a duplicate record.
---

# TEST: SECURITY-AA-15

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security application **** with a name parameter that is a duplicate record.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.add**" command followed by a name that is a duplicate record (for example: "Create-Application-Test")

```
> application.add Create-Application-Test
```

## Expected Behaviour

1- Should show : "Application secret: ..." followed by an Error message indicating that duplicate key value violates unique constraint.

```
> application.add Create-Application-Test
Application secret: 7524EE054493
E:System.Net.WebException: The remote server returned an error: (422) Unprocessable Entity.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (422) Unprocessable Entity.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error 23505: duplicate key value violates unique constraint "sec_app_app_pub_id_idx"
        2:The remote server returned an error: (422) Unprocessable Entity.
>
```
