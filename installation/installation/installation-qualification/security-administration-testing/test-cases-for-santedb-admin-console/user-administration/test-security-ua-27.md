---
description: Testing the user.info command with existing username provided as -u parameter.
---

# TEST: SECURITY-UA-27

## References

* [User Administration](../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)

## Discussion

The `user.info` command is for listing information about a user account and effective permissions with a single `-u` parameter for specifying a **username**.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/server-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.

## Actions/Steps

1\. Execute the `user.info` command with `-u` parameter specified as an existing username.

```
user.info -u <existing username>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.info -u demoadmin
Name: demoadmin
SID: 2a348c6e-c158-11ea-9f6f-00155d640b09
Email: administrator@santesuite.net
Phone:
Invalid Logins: 0
Lockout:
Last Login: 2021-07-13T09:45:48.7381950-04:00
Created: 2020-07-08T16:18:19.7545920-04:00 (Administrator)
Updated: 2021-07-13T09:45:48.7381950-04:00 (SYSTEM)
Roles: Test , TestyMcTester , TestGroup2 , ADMINISTRATORS , Muddsville
        Effective Policies:
                Unrestricted All [1.3.6.1.4.1.33349.3.1.5.9.2] : --- (default DENY)
                Unrestricted Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.0] : Grant (explicit)
                Change Password [1.3.6.1.4.1.33349.3.1.5.9.2.0.1] : Grant (inherited from Unrestricted Administrative Function)
                Administer Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.0.10] : Grant (inherited from Unrestricted Administrative Function)
                Access Audit Log [1.3.6.1.4.1.33349.3.1.5.9.2.0.11] : Grant (inherited from Unrestricted Administrative Function)
                Administer Applets [1.3.6.1.4.1.33349.3.1.5.9.2.0.12] : Grant (inherited from Unrestricted Administrative Function)
                Assign Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.13] : Grant (inherited from Unrestricted Administrative Function)
                Unrestricted PubSub Administration [1.3.6.1.4.1.33349.3.1.5.9.2.0.14] : Grant (inherited from Unrestricted Administrative Function)
                Create/Alter PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.1] : --- (default DENY)
                Disable/Enable PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.2] : --- (default DENY)
                Delete PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.3] : --- (default DENY)
                Read PubSub Subscriptions [1.3.6.1.4.1.33349.3.1.5.9.2.0.14.4] : --- (default DENY)
                Create Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.2] : Grant (inherited from Unrestricted Administrative Function)
                Alter Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.3] : Grant (inherited from Unrestricted Administrative Function)
                Create Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.4] : Grant (inherited from Unrestricted Administrative Function)
                Create Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1] : Grant (explicit)
                Create Device [1.3.6.1.4.1.33349.3.1.5.9.2.0.5] : Grant (inherited from Unrestricted Administrative Function)
                Create Application [1.3.6.1.4.1.33349.3.1.5.9.2.0.6] : Grant (inherited from Unrestricted Administrative Function)
                Administer Concept Dictionary [1.3.6.1.4.1.33349.3.1.5.9.2.0.7] : Grant (inherited from Unrestricted Administrative Function)
                Alter Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.8] : Grant (inherited from Unrestricted Administrative Function)
                Alter Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1] : Grant (explicit)
                Alter Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.9] : Grant (inherited from Unrestricted Administrative Function)
                Login [1.3.6.1.4.1.33349.3.1.5.9.2.1] : Grant (explicit)
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : Grant (inherited from Login)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : Grant (explicit)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : Grant (inherited from OAUTH Login)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : Grant (inherited from OAUTH Login)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : Grant (inherited from OAUTH Login)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : Grant (inherited from OAUTH Login)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : Grant (explicit)
                Allow Impersonation of Application [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2] : Elevate (explicit)
                Access Client Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.10] : Grant (explicit)
                Unrestricted Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2] : Grant (explicit)
                Query Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.0] : Grant (inherited from Unrestricted Clinical Data)
                Write Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.1] : Grant (inherited from Unrestricted Clinical Data)
                Delete Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.2] : Grant (inherited from Unrestricted Clinical Data)
                Read Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.3] : Grant (inherited from Unrestricted Clinical Data)
                Export Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.4] : Grant (inherited from Unrestricted Clinical Data)
                Elevate Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.5] : Grant (inherited from Unrestricted Clinical Data)
                Unrestricted Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4] : Grant (explicit)
                Read Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4.0] : Grant (inherited from Unrestricted Metadata)
                Read Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2] : --- (default DENY)
                Query Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3] : --- (default DENY)
                Read Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2] : --- (default DENY)
                Query Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3] : --- (default DENY)
                Write Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0] : Grant (inherited from Unrestricted Metadata)
                Delete Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1] : Grant (inherited from Unrestricted Metadata)
                Write Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0] : Grant (inherited from Unrestricted Metadata)
                Delete Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1] : Grant (inherited from Unrestricted Metadata)
                Unrestricted Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.5] : --- (default DENY)
                Write Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.0] : --- (default DENY)
                Delete Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.1] : --- (default DENY)
                Read Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.2] : --- (default DENY)
                Query Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.3] : --- (default DENY)
                Unrestricted MDM [1.3.6.1.4.1.33349.3.1.5.9.2.6] : Grant (explicit)
                Write MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.1] : Grant (inherited from Unrestricted MDM)
                Read MDM Locals [1.3.6.1.4.1.33349.3.1.5.9.2.6.2] : Grant (inherited from Unrestricted MDM)
                Merge MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.3] : Grant (inherited from Unrestricted MDM)
                Special Security Elevation [1.3.6.1.4.1.33349.3.1.5.9.2.600] : Elevate (explicit)
                Change Security Challenge Question [1.3.6.1.4.1.33349.3.1.5.9.2.600.1] : Elevate (inherited from Special Security Elevation)
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Deny (explicit)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                test [1.3.6.1.4.1.3349.3.1.5.9.2.99.3] : --- (default DENY)
                Create-Policy-Test [1.3.6.1.4.1.3349.3.1.5.9.2.99.4] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : Grant (explicit)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : Deny (explicit)
```

{% hint style="warning" %}
User information listed here may be outdated in the future and the list is subject to change.
{% endhint %}
