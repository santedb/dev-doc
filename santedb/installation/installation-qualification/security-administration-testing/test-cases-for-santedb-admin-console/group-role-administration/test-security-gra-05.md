---
description: Testing the role.info command with a existing role specified as -r parameter.
---

# TEST: SECURITY-GRA-05

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md) 

## Discussion

The `role.info` command is for listing a specific role's information and effective policies. The `-r` parameter is used to specify which **role **to display information and effective policies from.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role exists.

## Actions/Steps

1\. Execute the `role.` command with `-r` parameter specified as an existing role.

```
role.info -r <existing role name>
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```
> role.info -r ADMINISTRATORS
Name: ADMINISTRATORS
SID: f6d2ba1d-5bb5-41e3-b7fb-2ec32418b2e1
Description: Group for users who have administrative access test
Created: 2020-07-07T16:48:58.6930230-04:00 (SYSTEM)
Updated: 2021-04-05T14:09:41.7419680-04:00 (Administrator)
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
                Create Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1] : --- (default DENY)
                Create Device [1.3.6.1.4.1.33349.3.1.5.9.2.0.5] : Grant (inherited from Unrestricted Administrative Function)
                Create Application [1.3.6.1.4.1.33349.3.1.5.9.2.0.6] : Grant (inherited from Unrestricted Administrative Function)
                Administer Concept Dictionary [1.3.6.1.4.1.33349.3.1.5.9.2.0.7] : Grant (inherited from Unrestricted Administrative Function)
                Alter Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.8] : Grant (inherited from Unrestricted Administrative Function)
                Alter Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1] : --- (default DENY)
                Alter Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.9] : Grant (inherited from Unrestricted Administrative Function)
                Login [1.3.6.1.4.1.33349.3.1.5.9.2.1] : Grant (explicit)
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : Grant (inherited from Login)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : --- (default DENY)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : --- (default DENY)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : --- (default DENY)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : --- (default DENY)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : --- (default DENY)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : --- (default DENY)
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
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : Deny (explicit)
```

{% hint style="warning" %}
Role information listed here may be outdated in the future and the list is subject to change.
{% endhint %}
