# Application Administration

You can use the iCDR administrative console to create, list, lock, unlock and get information about applications within the iCDR instance.

## Viewing Applications

You can view applications in the system using the `application.list` command, specifying optional filter paramters.

```text
> application.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
010cc4e0-d8ff-11eb-8249-00155d640b09   Create-Application-Te...                                               0    *
ebb1fb1a-d8d1-11eb-8249-00155d640b09   test2                                                                  0    *
e30f0976-d8d1-11eb-8249-00155d640b09   test                                                                   0    *
a01a3472-d36f-11eb-8248-00155d640b09   Create-Application-Test                                                0    *
bc8221bc-9cbd-11eb-be65-00155d640b09   test-new4                                                              0    *
a9ada8ae-9cbd-11eb-be65-00155d640b09   test-new3                                                              0    *
```

The optional filter parameters for `application.list` ****are:

| Parameter | Description | Example |
| :--- | :--- | :--- |
| `-l` | Filter on locked status | `application.list -l` |
| `-a` | Include non-active application | `application.list -a` |

## Adding Applications

You can add an application to the iCDR instance using the `application.add` command and specifying the name you wish to give to the application.

{% hint style="info" %}
Application secret is shown after creation so that it can be copied and saved since it's not accessible later.
{% endhint %}

```text
> application.add Create-Application-Test-10
Application secret: D540A5CBB247
CREATE Create-Application-Test-10
>
```

The parameters for `application.add` are:

| Parameter | Description | Example |
| :--- | :--- | :--- |
| `-s` | The application secret to set | `application.add -s s3Cre+` |
| `-g` | The policies to grant deny application | `application.add -g 1.3.6.1.4.1.33349.3.1.5.9.2.999` |
| `-d` | The policies to deny the application | `application.add -d 1.3.6.1.4.1.33349.3.1.5.9.2.999` |
| `-n` | A description/note to add to the application | `application.add -n SPECIAL_APPLICATION_NOTE` |

## Locking/Unlocking Applications

To lock or unlock an application, the `application.lock` command with our without the `-l` flag to specify whether the lock should be set or unset.

To lock the application "Create-Application-Test":

```text
> application.lock -l Create-Application-Test
```

To unlock the application "Create-Application-Test":

```text
> application.lock Create-Application-Test
```

## Deleting/Undeleting Applications

To delete an application, the `application.del` command is used specifiying the application name.

To delete the application "Create-Application-Test":

```text
> application.del Create-Application-Test
```

To undelete an application, the `application.undel` command is used specifying the application name.

To undelete the application "Create-Application-Test":

```text
> application.undel Create-Application-Test
```

## Assigning Policies to an Application

To assign a policy to an application please visit 'Assigning Policies' section of [Policy Administration](policy-administration.md).

## Application Info View

You can get extended information about a particular application by using the `application.info` command and specifying the application name. For example, to get information about the application Create-Application-Test:

```text
> application.info Create-Application-Test
Name: Create-Application-Test
SID: a01a3472-d36f-11eb-8248-00155d640b09
Invalid Auth:
Lockout:
Last Auth:
Created: 2021-06-22T11:36:34.5714130-04:00 (demoadmin)
Updated: 2021-06-30T03:23:17.7651820-04:00 (Administrator)
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
                Create Local Users [1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1] : Grant (explicit)
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
                Override Disclosure [1.3.6.1.4.1.33349.3.1.5.9.2.999] : Deny (explicit)
                Restricted Information [1.3.6.1.4.1.33349.3.1.5.9.3] : --- (default DENY)
                Testy Mctesterson [1.3.6.1.4.1.66666.3.1.5.9.2.0.14] : --- (default DENY)
                SUPER SECRET DISCLOSURE [2.25.3049340304933] : --- (default DENY)
>
```

## 

