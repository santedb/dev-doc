---
description: Testing the role.add command with existing role provided as -r parameter only.
---

# TEST: SECURITY-GRA-08

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [Security Administration](../../../../../operations/security-administration/#demo-environment) 
* [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/)
* [TEST: SECURITY-GRA-01](test-security-gra-01.md)
* [TEST: SECURITY-GRA-02](test-security-gra-02.md) 

## Discussion

The `role.add` command is for adding a new role and has 1 required parameter that must pass validation: **role**. 

* The `-r` parameter is used to specify which **role** to display information and effective policies from.

## Pre-Conditions / Setup

1. Follow the directions from [Security Administration](../../../../../operations/security-administration/#demo-environment) to quickly setup and start using the [SanteDB Administration & Security Console](../../../../../operations/host-administration/santedb-icdr-admin-console/).
2. See [TEST: SECURITY-GRA-01](test-security-gra-01.md) and [TEST: SECURITY-GRA-02](test-security-gra-02.md) to check if a role does not exist.

## Actions/Steps

1. Execute the `role.add` command with `-r` parameter specified as non-existing role.

```text
role.add -r <new role name>
```

## Expected Behaviour

* Admin Console output should appear similar to the following:

```text
> role.add -r NewRole
>
```

* Check that the new role that was created appears:

```text
> role.list
SID                                    Name                 Description                                      A
c3ae21d2-fc23-4133-ba42-b0e0a3b817d7   SYSTEM               Group for user SYSTEM. Identifies the functio... *
dadbd858-13c5-44a3-ad7d-1c44cecaa4b6   ANONYMOUS            Group for user ANONYMOUS. Identifies the func... *
54b7677c-682b-425f-a937-3aa03d5951f1   SYNCHRONIZERS        Group for user SYNCHRONIZERS. Identifies the ... *
f5b58b94-e3ef-11eb-bbaf-eb1f1d969e16   NewRole                                                               *
f4e58ae8-8bbd-4635-a6d4-8a195b143436   USERS                Group for users who have login access test       *
57999738-e32d-11eb-bbaf-eb1f1d969e16   TEST01                                                                *
dcba17c0-e0ae-11eb-bbaf-eb1f1d969e16   NewRole4             NOTE/IS/LONGER/NOW                               *
8479182c-e0ae-11eb-bbaf-eb1f1d969e16   NewRole3             NOTE                                             *
40b2616c-e0ad-11eb-bbaf-eb1f1d969e16   TestRole3                                                             *
3c83672a-dfe1-11eb-bbae-eb1f1d969e16   Muddsville           A group for Muddsville residents and clinicians. *
86719164-e012-11eb-bbae-eb1f1d969e16   TestRole1                                                             *
9df881f4-e00c-11eb-bbae-eb1f1d969e16   TestGroup2           Checking Policies being added.                   *
613d05a0-dd0d-4516-a30c-e733741885f0   DEVICE               Represents a device in the system. Identifies... *
72fbf3f8-dfe1-11eb-bbae-eb1f1d969e16   TestGroup                                                             *
606e1586-dfe1-11eb-bbae-eb1f1d969e16   testGroup1                                                            *
c911ca0c-de82-11eb-bbad-eb1f1d969e16   Create-Role-Test1                                                     *
ff22744e-de81-11eb-bbad-eb1f1d969e16   Create-Role-Test                                                      *
0d605cd4-9642-11eb-be65-00155d640b09   TEST_REFACTOR        TEST                                             *
f6d2ba1d-5bb5-41e3-b7fb-2ec32418b2e1   ADMINISTRATORS       Group for users who have administrative acces... *
252b0ad6-88a9-11eb-be65-00155d640b09   newgroup             a new group edited again                         *
537cdc04-81ef-11eb-b733-00155d640b09   BoatFace             Testing with Boatface                            *
b81e78e0-8143-11eb-b733-00155d640b09   TestyMcTester        Test Group 1                                     *
801eeac0-6eff-11eb-92d2-00155d640b09   SENSITIVE_USERS      This group is for users which can see sensiti... *
43167dcb-6f77-4f37-8222-133e675b4434   CLINICAL_STAFF       Group for clinic staff                           *
```

{% hint style="warning" %}
Active roles listed here may be outdated in the future and the list is subject to change.
{% endhint %}

