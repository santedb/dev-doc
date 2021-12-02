---
description: Testing the successful assigning of a policy to an application.
---

# TEST: SECURITY-PA-03

## References

* [Policy Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/policy-administration.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when assigning policies to an application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**policy.assign**" command followed by object parameter:"**-a" (**or **"--application")** followed **** by the application(s) to assign the policy to followed by "**-p**" (or "**--policy**") followed by the policy(ies) to apply followed by "**-e**" (or "**--rule**") followed by the action to take (0/deny, 1/elevate, 2/grant).

{% hint style="info" %}
If you don't specify the action to take ("e" or "--rule" parameter) then the default action would be "deny".
{% endhint %}

```
> policy.assign -a Create-Application-Test -p 1.3.6.1.4.1.33349.3.1.5.9.2.999 -e 1
```

2- **Test Validation**: Use "**application.info**" command followed by application name.

```
> application.info Create-Application-Test
```

## Expected Behaviour

1- Should appear "the action (Deny or Elevate or Grant)"  followed by "policy name" followed by "application name".

```
> policy.assign -a Create-Application-Test -p 1.3.6.1.4.1.33349.3.1.5.9.2.999 -e 1
Elevate: Override Disclosure TO Create-Application-Test
>
```

2- Should the assigned policy ("Override Disclosure") appear in the Effective Policies row:

```
> application.info Create-Application-Test
Name: Create-Application-Test
SID: a01a3472-d36f-11eb-8248-00155d640b09
Invalid Auth:
Lockout:
Last Auth:
Created: 2021-06-22T11:36:34.5714130-04:00 (demoadmin)
Updated: 2021-07-05T03:17:09.1743860-04:00 (demoadmin)
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
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : Grant (explicit)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : Grant (inherited from Login as a Service)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : --- (default DENY)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : --- (default DENY)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : --- (default DENY)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : --- (default DENY)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : Grant (inherited from Login as a Service)
                Allow Impersonation of Application [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2] : Grant (inherited from Login as a Service)
                Access Client Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.10] : --- (default DENY)
                Unrestricted Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2] : Grant (explicit)
                Query Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.0] : Grant (inherited from Unrestricted Clinical Data)
                Write Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.1] : Grant (inherited from Unrestricted Clinical Data)
                Delete Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.2] : Grant (inherited from Unrestricted Clinical Data)
                Read Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.3] : Grant (inherited from Unrestricted Clinical Data)
                Export Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.4] : Grant (inherited from Unrestricted Clinical Data)
                Elevate Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.5] : Grant (inherited from Unrestricted Clinical Data)
                Unrestricted Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4] : Grant (explicit)
                Read Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4.0] : Grant (explicit)
                Read Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2] : Grant (inherited from Read Metadata)
                Query Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3] : Grant (inherited from Read Metadata)
                Read Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2] : Grant (inherited from Read Metadata)
                Query Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3] : Grant (inherited from Read Metadata)
                Write Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0] : Grant (inherited from Unrestricted Metadata)
                Delete Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1] : Grant (inherited from Unrestricted Metadata)
                Write Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0] : Grant (inherited from Unrestricted Metadata)
                Delete Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1] : Grant (inherited from Unrestricted Metadata)
                Unrestricted Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.5] : --- (default DENY)
                Write Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.0] : --- (default DENY)
                Delete Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.1] : --- (default DENY)
                Read Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.2] : --- (default DENY)
                Query Warehouse Data [1.3.6.1.4.1.33349.3.1.5.9.2.5.3] : --- (default DENY)
                Unrestricted MDM [1.3.6.1.4.1.33349.3.1.5.9.2.6] : --- (default DENY)
                Write MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.1] : --- (default DENY)
                Read MDM Locals [1.3.6.1.4.1.33349.3.1.5.9.2.6.2] : --- (default DENY)
                Merge MDM Master [1.3.6.1.4.1.33349.3.1.5.9.2.6.3] : --- (default DENY)
                Special Security Elevation [1.3.6.1.4.1.33349.3.1.5.9.2.600] : Elevate (explicit)
                Change Security Challenge Question [1.3.6.1.4.1.33349.3.1.5.9.2.600.1] : Elevate (inherited from Special Security Elevation)
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Elevate (explicit)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                Create-Policy-Test [1.3.6.1.4.1.3349.3.1.5.9.2.99.4] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
>
```
