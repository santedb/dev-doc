---
description: >-
  Testing the unsuccessful creation of a new device when device name parameter
  is a duplicate record.
---

# TEST: SECURITY-DA-14

## References

* [Device Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/untitled.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security device **** with a name parameter that is a duplicate record.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**device.add**" command followed by a name that is a duplicate record (for example: "Create-Device-Test")

```
> device.add Create-Device-Test
```

## Expected Behaviour

1- Should show : "Device secret: ..." followed by an Error message indicating that duplicate key value violates unique constraint.

```
> device.add Create-Device-Test
Device secret: 1B408BEACCE3C848B179CA6655F73964
E:System.Net.WebException: The remote server returned an error: (422) Unprocessable Entity.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (422) Unprocessable Entity.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error 23505: duplicate key value violates unique constraint "sec_dev_pub_id_idx"
        2:The remote server returned an error: (422) Unprocessable Entity.
>
```
