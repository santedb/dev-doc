---
description: >-
  Testing the successful assigning a policy to a role not specifying the action
  to take.
---

# TEST: SECURITY-PA-05

## References

* [Policy Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/policy-administration.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when assigning policies to a role not specifying the action to take.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**policy.assign**" command followed by "**-r" (**or** "--role") **followed** **by the role(s) to assign the policy to followed by "**-p**" (or "**--policy**") followed by the policy(ies) to apply.

{% hint style="info" %}
If you don't specify the action to take ("e" or "--rule" parameter) then the default action would be "deny".
{% endhint %}

```
> policy.assign -r Create-Role-Test -p 1.3.6.1.4.1.33349.3.1.5.9.2.999
```

2- **Test Validation**: Use "**role.info**" command followed  "**-r**" followed by role name.

```
> role.info -r Create-Role-Test
```

## Expected Behaviour

1- Should appear "Deny "  followed by "policy name" followed by "role name".

```
> policy.assign -r Create-Role-Test -p 1.3.6.1.4.1.33349.3.1.5.9.2.999
Deny: Override Disclosure TO Create-Role-Test
>
```

2- Should the assigned policy ("Override Disclosure") appear in the Effective Policies row with action : "Deny (explicit)"

```
> role.info -r Create-Role-Test
Name: Create-Role-Test
SID: ff22744e-de81-11eb-bbad-eb1f1d969e16
Description:
Created: 2021-07-06T13:45:48.1910570-04:00 (Administrator)
Updated: 2021-07-06T13:45:48.1910570-04:00 (Administrator)
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
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Deny (explicit)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                Create-Policy-Test [1.3.6.1.4.1.3349.3.1.5.9.2.99.4] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
>
```
