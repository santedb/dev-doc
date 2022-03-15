# SOP: User Lockout

## Summary

This standard operating procedure is intended to illustrate the process for unlocking a user account, and resetting the user's password.&#x20;

### Use Procedure When

* [ ] There has been a support ticket for a locked out user account raised
* [ ] There has been a notice (from the administration console) of repeated, invalid attempts to access the system

## Procedure

### Before Beginning

* [ ] Validate that the request to unlock the account has been made by the user owning the account
  * [ ] Validate the user's telephone number or e-mail address on file (contact the user if necessary)
  * [ ] Validate the user's demographic information with the information on the CDR user administration screen.
* [ ] Document (in the helpdesk or other shared note area) that the user account has been locked, the length of lock and the number of invalid logins
* [ ] Note the user which has locked the account (`SYSTEM` indicates invalid access attempt lock or other system security lock, whereas a user name indicates another administrative user has locked the account)
* [ ] Your account has the **Alter Identity** permission

### Procedures / Tasks

1. Access the SanteDB administrative portal by [logging-in.md](../../cdr-administration/santedb-administration-panel/logging-in.md "mention")
2. Visit the [security-administration](../../cdr-administration/santedb-administration-panel/security-administration/ "mention") center
3. Click on the [#user-list](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md#user-list "mention") and search for the user using the system login name
4. Press the `Edit` button to access the [#editing-security-settings](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md#editing-security-settings "mention") screen
5. Press the `Reset` button next to the `Invalid Login Attempts` field and confirm
6. (Optional) Press the `Reset PWD` button and assign a new, random password
7. Press the `Unlock` button next to the lockout information and confirm

### After Completion

* [ ] Note the time and procedure in the security log (if available)
* [ ] Notify the user and/or user supervisor of the unlock event and (if changed) the new password.

## Summary Information

**Current Status:**  Example\
**Reviewed By:** SanteSuite Team

### **Revision History**

| Author                   | Date       | Changes         |
| ------------------------ | ---------- | --------------- |
| Justin Fyfe (SanteSuite) | 2022-01-11 | Initial Version |
|                          |            |                 |
|                          |            |                 |

### See Also

{% content-ref url="../../cdr-administration/santedb-administration-panel/security-administration/" %}
[security-administration](../../cdr-administration/santedb-administration-panel/security-administration/)
{% endcontent-ref %}

{% content-ref url="../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md" %}
[managing-user-accounts.md](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md)
{% endcontent-ref %}
