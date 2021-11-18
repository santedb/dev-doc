---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  and duplicate policy both denied and granted explicitly as -g and -d
  parameters.
---

# TEST: SECURITY-GRA-11

## References

* [Group / Role Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md)
* [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md)&#x20;

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**.&#x20;

* The `-r` parameter is used to specify which **role** to display information and effective policies from.
* The `-g` parameter is used to specify which **policy **to explicitly grant the new role being added.
* The `-d` parameter is used to specify which **policy **to explicitly deny the new role being added.
* An exception is thrown when a duplicate policy is both granted and denied in the same command.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.
3. See [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) for checking if a policy exists.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as non-existing role and with both `-d` and `-g` parameters specified as an identical existing policy.

```
role.add -r <new role name> -d 1.3.6.1.4.1.33349.3.1.5.9.2.999 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999 
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```
> role.add -r TestRole03 -d 1.3.6.1.4.1.33349.3.1.5.9.2.999 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999
E:System.Net.WebException: The remote server returned an error: (422) Unprocessable Entity.
   at SanteDB.Server.Core.Http.RestClient.InvokeInternal[TBody,TResult](String method, String url, String contentType, WebHeaderCollection requestHeaders, WebHeaderCollection& responseHeaders, TBody body, NameValueCollection query)
E:Error invoking HTTP: The remote server returned an error: (422) Unprocessable Entity.
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error 23505: duplicate key value violates unique constraint "sec_pol_rol_assoc_pol_rol_idx"
        2:The remote server returned an error: (422) Unprocessable Entity.
```
