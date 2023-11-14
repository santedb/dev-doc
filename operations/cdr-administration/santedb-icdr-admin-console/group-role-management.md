# Group / Role Administration

You can use the iCDR administrative console to view, add, list, and get information about groups/roles within the iCDR instance.

## Viewing Groups/Roles

You can view groups/role in the system using the `role.list` command, specifying optional filter parameters.

```
> role.list
SID                                    Name                 Description                                      A
dadbd858-13c5-44a3-ad7d-1c44cecaa4b6   ANONYMOUS            Group for user ANONYMOUS. Identifies the func... *
54b7677c-682b-425f-a937-3aa03d5951f1   SYNCHRONIZERS        Group for user SYNCHRONIZERS. Identifies the ... *
c3ae21d2-fc23-4133-ba42-b0e0a3b817d7   SYSTEM               Group for user SYSTEM. Identifies the functio... *
3c83672a-dfe1-11eb-bbae-eb1f1d969e16   Muddsville           A group for Muddsville residents and clinicians. *
86719164-e012-11eb-bbae-eb1f1d969e16   TestRole1                                                             *
9df881f4-e00c-11eb-bbae-eb1f1d969e16   TestGroup2           Checking Policies being added.                   *
613d05a0-dd0d-4516-a30c-e733741885f0   DEVICE               Represents a device in the system. Identifies... *
72fbf3f8-dfe1-11eb-bbae-eb1f1d969e16   TestGroup                                                             *
606e1586-dfe1-11eb-bbae-eb1f1d969e16   testGroup1                                                            *
c911ca0c-de82-11eb-bbad-eb1f1d969e16   Create-Role-Test1                                                     *
ff22744e-de81-11eb-bbad-eb1f1d969e16   Create-Role-Test                                                      *
0d605cd4-9642-11eb-be65-00155d640b09   TEST_REFACTOR        TEST                                             *
f4e58ae8-8bbd-4635-a6d4-8a195b143436   USERS                Group for users who have login access test       *
f6d2ba1d-5bb5-41e3-b7fb-2ec32418b2e1   ADMINISTRATORS       Group for users who have administrative acces... *
252b0ad6-88a9-11eb-be65-00155d640b09   newgroup             a new group edited again                         *
537cdc04-81ef-11eb-b733-00155d640b09   BoatFace             Testing with Boatface                            *
b81e78e0-8143-11eb-b733-00155d640b09   TestyMcTester        Test Group 1                                     *
801eeac0-6eff-11eb-92d2-00155d640b09   SENSITIVE_USERS      This group is for users which can see sensiti... *
43167dcb-6f77-4f37-8222-133e675b4434   CLINICAL_STAFF       Group for clinic staff                           *
```

The optional filter parameters for `role.list` are:

| Parameter | Description                           | Example        |
| --------- | ------------------------------------- | -------------- |
| `-a`      | Show non-active (deleted) roles only. | `role.list -a` |

## Adding Group/Role

You can add a group/role to the iCDR instance using the `role.add` command with required `-r` parameter for group/role name:

```
role.add -r NewRoleTest
```

The optional filter parameters for `role.add` are.

| Parameter | Description                                          | Example                                                       |
| --------- | ---------------------------------------------------- | ------------------------------------------------------------- |
| `-g`      | Specify a policy to explicitly grant the group/role. | `role.add -r NewRoleTest1 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999` |
| `-d`      | Specify a policy to explicitly deny the group/role.  | `role.add -r NewRoleTest2 -d 1.3.6.1.4.1.33349.3.1.5.9.2.999` |
| `-n`      | Set the Description core property for a group/role.  | `role.add -r NewRoleTest2 -n NO_SPACES_NOTE`                  |

## Viewing Group/Role Information

You can view groups/role information for a specific group/role to see all properties and policies using the `role.info` command with required `-r` parameter for group/role name:

```
> role.info -r NewRole3
Name: NewRole3
SID: 8479182c-e0ae-11eb-bbaf-eb1f1d969e16
Description: NOTE
Created: 2021-07-09T08:09:31.9175110-04:00 (Administrator)
Updated: 2021-07-09T08:10:44.9203880-04:00 (Administrator)
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
                Create-Policy-Test [1.3.6.1.4.1.3349.3.1.5.9.2.99.4] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
```

There are no optional filter parameters for `role.list`.

##
