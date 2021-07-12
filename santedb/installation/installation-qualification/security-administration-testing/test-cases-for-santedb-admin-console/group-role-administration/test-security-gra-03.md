---
description: Testing the role.info command with no parameters specified.
---

# TEST: SECURITY-GRA-03

## References

* [Group / Role Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/group-role-management.md)
* [User Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/user-administration.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when changing roles for a user.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**user.roles**" command followed by "**-u"** followed ****by the username of the user \(for example: Bob\) followed by "**-r**" followed by the role/s to assign to the user.

```text
> user.roles -u Bob -r Create-Role-Test
```

2- **Test Validation**: Use "**user.info**" command  followed by user name.

```text
> user.info Bob
```

## Expected Behaviour

1- Should 

```text
> user.roles -u Bob -r Create-Role-Test
>
```

2- Should appear  "Roles" row with the value : &lt;the role you assigned&gt;

```text
> user.info Bob
Name: Bob
SID: 54558ca3-c093-11ea-9f6f-00155d640b09
Email: bob@marc-hi.ca
Phone: tel:+19055751212;ext=4085
Invalid Logins: 0
Lockout:
Last Login:
Created: 2020-07-07T16:49:19.5797190-04:00 (SYSTEM)
Updated: 2021-07-06T17:52:37.4082400-04:00 (Administrator)
Roles: Create-Role-Test
        Effective Policies:
```



