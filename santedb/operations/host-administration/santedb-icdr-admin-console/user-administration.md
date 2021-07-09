# User Administration

You can use the iCDR administrative console to create, list, lock and get information about users within the iCDR instance.

## Viewing Users

You can view users in the system using the `user.list` command, specifying optional filter parameters.

```text
> user.list
SID                                    Name                     Last Auth              Lockout                ILA  A
fadca076-3690-4a6e-af9e-f1cd68e8c7e8   SYSTEM                                                                 0    *
c96859f0-043c-4480-8dab-f69d6e86696c   ANONYMOUS                                                              0    *
54558ca2-c093-11ea-9f6f-00155d640b09   Administrator            2021-02-21T17:08:57...                        0    *
2a348c6e-c158-11ea-9f6f-00155d640b09   demoadmin                2021-02-19T15:07:50...                        0    *
54558ca4-c093-11ea-9f6f-00155d640b09   Allison                  2021-02-16T12:00:31... 9999-12-21T18:59:59... 2    *
54558ca3-c093-11ea-9f6f-00155d640b09   Bob                                             9999-12-21T18:59:59... 0    *
```

The optional filter parameters for `user.list` are.

| Parameter | Description | Example |
| :--- | :--- | :--- |
| `-h` | Shows only HUMAN users and hides system users. | `user.list -h` |
| `-s` | Shows only SYSTEM users and hides human users. | `user.list -s` |
| `-u` | Filters by a specific user name pattern | `user.list -u Bob` |

## Adding Users

You can add a user to the iCDR instance using the `user.add` command:

```text
> user.add -r CLINICAL_STAFF -u console -e user@user.com -p @Testing123
```

You may receive an error from the server, if this is the case the server will indicate the reason for the failure, for example, when adding a user where the specified password does not match the minimum password requirements:

```text
> user.add -r CLINICAL_STAFF -u baduser -e bad@user.com -p blah
ERR: Exception has been thrown by the target of an invocation.
        1:The remote server returned an error: (422) Unprocessable Entity.
                REMOTE: Exception of type 'SanteDB.Core.Exceptions.DetectedIssueException' was thrown.
                REMOTE: RULE: Error Password failed validation
        2:The remote server returned an error: (422) Unprocessable Entity.
```

| Parameter | Description | Example |
| :--- | :--- | :--- |
| `-r` | The role\(s\) to assign the user | `-r CLINICAL_STAFF -r VIP` |
| `-u` | The username of the user | `-u BOB` |
| `-e` | The security e-mail address of the user | `-e foo@foo.com` |
| `-p` | The initial password to set for the user | `-p P@ssw0rd` |

## Locking Users

To lock or unlock a user, the `user.lock` command is used specifying whether the lock should be set or unset.

To unlock the user bob:

```text
user.lock bob
```

To lock the user bob:

```text
user.lock -l bob
```

## User Info View

You can get extended information about a particular user by using the `user.info` command and specifying the username. For example, to get information about user bob:

```text
> user.info allison
Name: Allison
SID: 54558ca4-c093-11ea-9f6f-00155d640b09
Email: allison@marc-hi.ca
Phone: tel:+19055751212;ext=4085
Invalid Logins: 2
Lockout: 9999-12-21T18:59:59.9999990-05:00
Last Login: 2021-02-16T12:00:31.2499360-05:00
Created: 2020-07-07T16:49:19.5797190-04:00 (SYSTEM)
Updated: 2021-02-16T17:42:36.4142670-05:00 (Administrator)
Roles: CLINICAL_STAFF , SENSITIVE_USERS
        Effective Policies:
                Unrestricted All [1.3.6.1.4.1.33349.3.1.5.9.2] : --- (default DENY)
                Unrestricted Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.0] : Deny (explicit)
                Change Password [1.3.6.1.4.1.33349.3.1.5.9.2.0.1] : Deny (inherited from Unrestricted Administrative Function)
                Administer Data Warehouse [1.3.6.1.4.1.33349.3.1.5.9.2.0.10] : Deny (inherited from Unrestricted Administrative Function)
                Access Audit Log [1.3.6.1.4.1.33349.3.1.5.9.2.0.11] : Deny (inherited from Unrestricted Administrative Function)
                Administer Applets [1.3.6.1.4.1.33349.3.1.5.9.2.0.12] : Deny (inherited from Unrestricted Administrative Function)
                Assign Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.13] : Deny (inherited from Unrestricted Administrative Function)
                Create Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.2] : Deny (inherited from Unrestricted Administrative Function)
                Alter Role [1.3.6.1.4.1.33349.3.1.5.9.2.0.3] : Deny (inherited from Unrestricted Administrative Function)
                Create Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.4] : Deny (inherited from Unrestricted Administrative Function)
                Create Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1] : --- (default DENY)
                Create Device [1.3.6.1.4.1.33349.3.1.5.9.2.0.5] : Deny (inherited from Unrestricted Administrative Function)
                Create Application [1.3.6.1.4.1.33349.3.1.5.9.2.0.6] : Elevate (explicit)
                Administer Concept Dictionary [1.3.6.1.4.1.33349.3.1.5.9.2.0.7] : Deny (inherited from Unrestricted Administrative Function)
                Alter Identity [1.3.6.1.4.1.33349.3.1.5.9.2.0.8] : Deny (inherited from Unrestricted Administrative Function)
                Alter Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1] : --- (default DENY)
                Alter Policy [1.3.6.1.4.1.33349.3.1.5.9.2.0.9] : Deny (inherited from Unrestricted Administrative Function)
                Login [1.3.6.1.4.1.33349.3.1.5.9.2.1] : Grant (explicit)
                Login as a Service [1.3.6.1.4.1.33349.3.1.5.9.2.1.0] : Grant (inherited from Login)
                OAUTH Login [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0] : --- (default DENY)
                OAUTH client_credentials flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1] : --- (default DENY)
                OAUTH password flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2] : --- (default DENY)
                OAUTH authoization code grant flow permission [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3] : --- (default DENY)
                OAUTH Password Reset grant (extended permission) [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4] : --- (default DENY)
                Login for Password Reassignment [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1] : --- (default DENY)
                Allow Impersonation of Application [1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2] : --- (default DENY)
                Access Client Administrative Function [1.3.6.1.4.1.33349.3.1.5.9.2.10] : --- (default DENY)
                Unrestricted Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2] : Grant (explicit)
                Query Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.0] : Grant (inherited from Unrestricted Clinical Data)
                Write Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.1] : Grant (inherited from Unrestricted Clinical Data)
                Delete Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.2] : Grant (inherited from Unrestricted Clinical Data)
                Read Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.3] : Grant (inherited from Unrestricted Clinical Data)
                Export Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.4] : Grant (inherited from Unrestricted Clinical Data)
                Elevate Clinical Data [1.3.6.1.4.1.33349.3.1.5.9.2.2.5] : Grant (inherited from Unrestricted Clinical Data)
                Unrestricted Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4] : --- (default DENY)
                Read Metadata [1.3.6.1.4.1.33349.3.1.5.9.2.4.0] : Grant (explicit)
                Read Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2] : Grant (inherited from Read Metadata)
                Query Materials [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3] : Grant (inherited from Read Metadata)
                Read Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2] : Grant (inherited from Read Metadata)
                Query Places & Orgs [1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3] : Grant (inherited from Read Metadata)
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
                Special Security Elevation [1.3.6.1.4.1.33349.3.1.5.9.2.600] : Deny (explicit)
                Change Security Challenge Question [1.3.6.1.4.1.33349.3.1.5.9.2.600.1] : Deny (inherited from Special Security Elevation)
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Deny (explicit)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : Grant (explicit)
```

