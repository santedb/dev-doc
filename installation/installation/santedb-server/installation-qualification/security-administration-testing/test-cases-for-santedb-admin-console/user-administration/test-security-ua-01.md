---
description: Testing the user.list command without specifying additional parameters.
---

# TEST: SECURITY-UA-01

## References

* [User Administration](../../../../../../../operations/server-administration/santedb-icdr-admin-console/user-administration.md)
* [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment)&#x20;
* [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/)

## Discussion

The `user.list` command is for listing users.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../../../operations-1/system-administration/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../../../operations/server-administration/santedb-icdr-admin-console/).

## Actions/Steps

1\. Execute the `user.list` command.

```
user.list
```

## Expected Behaviour

* The Admin Console output should appear similarly to the following:

```
> user.list
SID                                    Name                     Last Auth              Lockout                ILA  A
c96859f0-043c-4480-8dab-f69d6e86696c   ANONYMOUS                                                              0    *
fadca076-3690-4a6e-af9e-f1cd68e8c7e8   SYSTEM                                                                 0    *
54558ca2-c093-11ea-9f6f-00155d640b09   Administrator            2021-07-09T10:08:38...                        0    *
2a348c6e-c158-11ea-9f6f-00155d640b09   demoadmin                2021-07-09T08:30:59...                        0    *
f3ace62a-dda6-11eb-bbad-eb1f1d969e16   ClinicalStaffUser123     2021-07-04T21:58:45...                        0    *
54558ca3-c093-11ea-9f6f-00155d640b09   Bob                                             9999-12-21T18:59:59... 0    *
25a4f67a-df20-11eb-bbad-eb1f1d969e16   UserTest01                                                             0    *
52c42172-df1a-11eb-bbad-eb1f1d969e16   ClinicalStaffUser12                                                    0    *
a762c780-df18-11eb-bbad-eb1f1d969e16   ClinicalStaffUser11                                                    0    *
54558ca4-c093-11ea-9f6f-00155d640b09   Allison                  2021-02-15T21:00:31... 2021-03-15T10:15:36... 9    *
3dd0d1c6-75ba-11eb-b733-00155d640b09   Dr_Quinn                 2021-02-19T20:34:06...                        0    *
98d6e9fc-7493-11eb-b733-00155d640b09   console                                                                0    *
```

{% hint style="warning" %}
Users listed here may be outdated in the future and the list is subject to change.
{% endhint %}
