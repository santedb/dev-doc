---
description: >-
  Testing the role.add command with non-existing role provided as -r parameter
  and descripton/note provided as -n parameter.
---

# TEST: SECURITY-GRA-14

## References

* [Group / Role Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md)
* [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md)&#x20;

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**.&#x20;

* The `-r` parameter is used to specify which **role** to display information and effective policies from.
* The `-g` parameter is used to specify which **policy** to explicitly grant the new role being added.
* The `-d` parameter is used to specify which **policy** to explicitly deny the new role being added.
* The `-n` parameter is used to specify a **description/note** (no spaces).&#x20;

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.
3. See [TEST: SECURITY-PA-01](../policy-administration-tests/test-security-pa-01.md) for checking if a policy exists.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as non-existing role and `-n` parameter specified as a description/note without spaces.

```
role.add -r <new role name> -n SPECIAL_ROLE_NOTE
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```
> role.add -r TestRole03 -n SPECIAL_ROLE_NOTE
>
```

* Check that the role created has the specified Description property:

```
> role.info -r TestRole03
Name: TestRole03
SID: 4adda038-e3f1-11eb-bbaf-eb1f1d969e16
Description: SPECIAL_ROLE_NOTE
Created: 2021-07-13T11:45:05.1131570-04:00 (Administrator)
Updated: 2021-07-13T11:48:38.9308250-04:00 (Administrator)
        Effective Policies:
                Unrestricted All [1.3.6.1.4.1.33349.3.1.5.9.2] : --- (default DENY)
                Unrestricted Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.0] : --- (default DENY)
                Change Password [1.3.6.1.4.1.33349.3.1.5.9.2.0.1] : --- (default DENY)
                Administer Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.0.10] : --- (default DENY)
                Access Audit Log [1.3.6.1.4.1.33349.3.1.5.9.2.0.11] : --- (default DENY)
                Administer Applets [1.3.6.1.4.1.33349.3.1.5.9.2.0.12] : --- (default DENY)
                Assign Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.13] : --- (default DENY)
                Unrestricted PubSub Administration [1.3.6.1.4.1.33349.3.1.5.9.2.0.14] : --- (default DENY)
                Create/Alter PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.1] : --- (default DENY)
                Disable/Enable PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.2] : --- (default DENY)
                Delete PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.3] : --- (default DENY)
                Read PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.4] : --- (default DENY)
                Create Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.2] : --- (default DENY)
                Alter Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.3] : --- (default DENY)
                Create Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.4] : --- (default DENY)
                Create Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1] : --- (default DENY)
                Create Device [1.3.6.1.4.1.33349.3.1.5.9.2.0.5] : --- (default DENY)
                Create Application [1.3.6.1.4.1.33349.3.1.5.9.2.0.6] : --- (default DENY)
                Administer Concept Dictionary [1.3.6.1.4.1.33349.3.1.5.9.2.0.7] : --- (default DENY)
                Alter Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.8] : --- (default DENY)
                Alter Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1] : --- (default DENY)
                Alter Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.9] : --- (default DENY)
                Login [1.3.6.1.4.1.33349.3.1.5.9.2.1] : --- (default DENY)
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : --- (default DENY)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : --- (default DENY)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : --- (default DENY)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : --- (default DENY)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : --- (default DENY)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : --- (default DENY)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : --- (default DENY)
                Allow Impersonation of Application [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2] : --- (default DENY)
                Access Client Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.10] : --- (default DENY)
                Unrestricted Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2] : --- (default DENY)
                Query Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.0] : --- (default DENY)
                Write Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.1] : --- (default DENY)
                Delete Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.2] : --- (default DENY)
                Read Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.3] : --- (default DENY)
                Export Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.4] : --- (default DENY)
                Elevate Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.5] : --- (default DENY)
                Unrestricted Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4] : --- (default DENY)
                Read Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4.0] : --- (default DENY)
                Read Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2] : --- (default DENY)
                Query Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3] : --- (default DENY)
                Read Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2] : --- (default DENY)
                Query Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3] : --- (default DENY)
                Write Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0] : --- (default DENY)
                Delete Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1] : --- (default DENY)
                Write Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0] : --- (default DENY)
                Delete Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1] : --- (default DENY)
                Unrestricted Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.5] : --- (default DENY)
                Write Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.0] : --- (default DENY)
                Delete Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.1] : --- (default DENY)
                Read Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.2] : --- (default DENY)
                Query Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.3] : --- (default DENY)
                Unrestricted MDM [1.3.6.1.4.1.33349.3.1.5.9.2.6] : --- (default DENY)
                Write MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.1] : --- (default DENY)
                Read MDM Locals [1.3.6.1.4.1.33349.3.1.5.9.2.6.2] : --- (default DENY)
                Merge MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.3] : --- (default DENY)
                Special Security Elevation [1.3.6.1.4.1.33349.3.1.5.9.2.600] : --- (default DENY)
                Change Security Challenge Question [1.3.6.1.4.1.33349.3.1.5.9.2.600.1] : --- (default DENY)
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : --- (default DENY)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                test [1.3.6.1.4.1.3349.3.1.5.9.2.99.3] : --- (default DENY)
                Create-Policy-Test [1.3.6.1.4.1.3349.3.1.5.9.2.99.4] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
```

{% hint style="warning" %}
Role information listed here may be outdated in the future and the list is subject to change.
{% endhint %}
