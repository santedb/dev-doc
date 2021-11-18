---
description: >-
  Testing the user.roles command with existing username provided as -u parameter
  and with valid role provided as -r parameter.
---

# TEST: SECURITY-UA-40

## References

* [User Administration](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-UA-02](test-security-ua-02.md)
* [TEST: SECURITY-UA-03](test-security-ua-03.md)
* [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md)
* [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md)

## Discussion

The `user.roles` command is for assigning roles to a user.&#x20;

* The `-u` parameter is used to specify the **username **of which user to assign roles to.&#x20;
* The `-r` parameter is used to specify which **role** to assign to the specified user.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../operations/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../operations/system-administration/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-UA-02](test-security-ua-02.md) or [TEST: SECURITY-UA-03](test-security-ua-03.md) for checking if a username exists.
3. See [TEST: SECURITY-GRA-04](../group-role-administration/test-security-gra-04.md) or [TEST: SECURITY-GRA-05](../group-role-administration/test-security-gra-05.md) for checking if a role exists.

## Actions/Steps

1\.  Execute the `user.roles` command with `-u` parameter specified as an existing user and `-r` parameter specified as an existing role.

```
user.roles -u <existing username> -r <existing role>
```

## Expected Behaviour

* Admin Console output should appear as follows:

```
> user.roles -u TestUser123 -r USERS
>
```

* Check that all other roles are removed and only the one assigned appears:

```
> user.info -u TestUser123
Name: TestUser123
SID: 6f25da3a-e3da-11eb-bbaf-eb1f1d969e16
Email:
Phone:
Invalid Logins: 2
Lockout:
Last Login: 2021-07-13T06:54:26.0542210-04:00
Created: 2021-07-13T09:01:27.1885800-04:00 (Administrator)
Updated: 2021-07-13T11:03:26.1709380-04:00 (Administrator)
Roles: USERS
        Effective Policies:
                Unrestricted All [1.3.6.1.4.1.33349.3.1.5.9.2] : Deny (explicit)
                Unrestricted Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.0] : Deny (inherited from Unrestricted All)
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
                Login [1.3.6.1.4.1.33349.3.1.5.9.2.1] : Grant (explicit)
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : Grant (inherited from Login)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : Grant (explicit)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : Grant (inherited from OAUTH Login)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : Grant (inherited from OAUTH Login)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : Grant (inherited from OAUTH Login)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : Grant (inherited from OAUTH Login)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : --- (default DENY)
                Allow Impersonation of Application [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2] : --- (default DENY)
                Access Client Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.10] : Deny (inherited from Unrestricted All)
                Unrestricted Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2] : Deny (inherited from Unrestricted All)
                Query Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.0] : --- (default DENY)
                Write Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.1] : --- (default DENY)
                Delete Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.2] : --- (default DENY)
                Read Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.3] : --- (default DENY)
                Export Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.4] : --- (default DENY)
                Elevate Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.5] : --- (default DENY)
                Unrestricted Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4] : Deny (inherited from Unrestricted All)
                Read Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4.0] : --- (default DENY)
                Read Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2] : --- (default DENY)
                Query Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3] : --- (default DENY)
                Read Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2] : --- (default DENY)
                Query Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3] : --- (default DENY)
                Write Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0] : --- (default DENY)
                Delete Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1] : --- (default DENY)
                Write Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0] : --- (default DENY)
                Delete Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1] : --- (default DENY)
                Unrestricted Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.5] : Deny (inherited from Unrestricted All)
                Write Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.0] : --- (default DENY)
                Delete Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.1] : --- (default DENY)
                Read Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.2] : --- (default DENY)
                Query Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.3] : --- (default DENY)
                Unrestricted MDM [1.3.6.1.4.1.33349.3.1.5.9.2.6] : Deny (inherited from Unrestricted All)
                Write MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.1] : --- (default DENY)
                Read MDM Locals [1.3.6.1.4.1.33349.3.1.5.9.2.6.2] : --- (default DENY)
                Merge MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.3] : --- (default DENY)
                Special Security Elevation [1.3.6.1.4.1.33349.3.1.5.9.2.600] : Deny (inherited from Unrestricted All)
                Change Security Challenge Question [1.3.6.1.4.1.33349.3.1.5.9.2.600.1] : --- (default DENY)
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Deny (inherited from Unrestricted All)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                test [1.3.6.1.4.1.3349.3.1.5.9.2.99.3] : --- (default DENY)
                Create-Policy-Test [1.3.6.1.4.1.3349.3.1.5.9.2.99.4] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
```

{% hint style="warning" %}
User information listed here may be outdated in the future and the list is subject to change.
{% endhint %}
