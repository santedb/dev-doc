# TEST: SECURITY-GRA-02

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new role.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**role.add**" command followed by "**-r"** followed ****by the name you wish to give to the role. \(For instance "Create-Role-Test"\)

```text
> role.add -r Create-Role-Test
```



2- To test the  validation of the created role use "**role.list**" command \(This command lists all the roles \)

```text
> role.list
```

## Expected Behaviour

1- Should

```text
> role.add -r Create-Role-Test
>
```

2- Should the newly created role appear\("Create-Role-Test"\) on the list of roles.

```text
> role.list
SID                                    Name                 Description                                      A
c3ae21d2-fc23-4133-ba42-b0e0a3b817d7   SYSTEM               Group for user SYSTEM. Identifies the functio... *
dadbd858-13c5-44a3-ad7d-1c44cecaa4b6   ANONYMOUS            Group for user ANONYMOUS. Identifies the func... *
54b7677c-682b-425f-a937-3aa03d5951f1   SYNCHRONIZERS        Group for user SYNCHRONIZERS. Identifies the ... *
613d05a0-dd0d-4516-a30c-e733741885f0   DEVICE               Represents a device in the system. Identifies... *
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



