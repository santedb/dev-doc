# Deactivating Users

## Summary

This standard operating procedure intends to guide system administrators through the process of deactivating a user.&#x20;

### Use Procedure When

* [ ] A user account needs to be removed from the CDR
* [ ] A user account has been detected as breached
* [ ] A request to deactivate a user account has been received by the administrator

## Procedure

### Before Beginning

* [ ] There has been received, documentation of why the account is or needs to be deactivated, including:
  * [ ] Notice of termination of the user's employment or contractual relationship
  * [ ] Notice of a security breach or misuse of the system
  * [ ] Notice of employment change or duty change
* [ ] The e-mail address for the user account in question has been notified of the deactivation (or pending deactivation)
* [ ] The administrator has collected the username (system login name) of the user to be deactivated.

### Procedures / Tasks

1. Access the SanteDB administrative portal by [logging-in.md](../../cdr-administration/santedb-administration-panel/logging-in.md "mention")
2. Visit the [security-administration](../../cdr-administration/santedb-administration-panel/security-administration/ "mention") center
3. Click on the [#user-list](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md#user-list "mention") and search for the user using the system login name
4. Click the `Lock` button to lock out the user (to prevent un-deletion from restoring the user's access)
5. Click the `Delete` button and confirm that the user account is to be deleted

## Summary Information

**Current Status:** Example\
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
