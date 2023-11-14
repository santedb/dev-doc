# SOP: Onboarding Users

## Summary

This standard operating procedure (SOP) should be used when an implementing jurisdiction's administrator wishes to add a new user to the SanteDB implementation.&#x20;

### Use Procedure When

* [ ] You are a system administrator for the jurisdictional deployment of the SanteDB infrastructure
* [ ] There has been a request made (and approved by a supervisor) to add a new user to the SanteDB infrastructure
* [ ] The user, or relevant supervisor has submitted the appropriate documentation for the new user.

## Procedure

### Before Beginning

* [ ] Establish the user has a valid reason for accessing the SanteDB system
  * [ ] The user is a clinician who requires access to SanteDB's clinical data
  * [ ] The user is an administrator or support person who requires access to the administrative solution
  * [ ] The user is a supervisor requiring access to management data, or cohort data.
* [ ] Collect legal/compliance information for your jurisdiction, including:
  * [ ] Government issued photo identification showing the new user's name, address, and other demographics details.
  * [ ] The new user's employment details including division, employer, and citizenship.
* [ ] Establish the correct level of access for the user
  * [ ] The user will require access to administrative functions (`ADMINISTRATORS`)
  * [ ] The user will require access to clinical data functions (`CLINICAL_STAFF`)
  * [ ] The user will require access to reports (...)
* [ ] Collect and verify appropriate contact information for the new user
  * [ ] The user's telephone number (where they can be contacted for OTP and auditing/compliance reasons)
  * [ ] The user's e-mail address (where they can be contacted for OTP and auditing/compliance reasons)
* [ ] Determine a unique user name for the new user, in the format `familyNamefirstInitial` (for example: Bob Smith becomes `smithb` , subsequent Bob Smiths become `smithb1`, `smithb2`, etc.)
* [ ] Your user account has the **Create Identity** policy granted

### Procedures / Tasks

1. Access the SanteDB Administrative Portal by[logging-in.md](../../cdr-administration/santedb-administration-panel/logging-in.md "mention")
2. Access the [security-administration](../../cdr-administration/santedb-administration-panel/security-administration/ "mention") menu item
3. Click on the [#user-list](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md#user-list "mention") , and press `Create`
4. Input the collected information for the user on the [#creating-user-accounts](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md#creating-user-accounts "mention")
   1. Input the user's new user name as determined above.
   2. Assign the appropriate roles as determine in the pre-steps of this procedure.
   3. Create a random password (to be shared with the user)
   4. Input the user's profile information such as legal name, e-mail and telephone number, the user's preferred language, their assigned facility and primary employer.
5. Press the `Save` button

### After Completion

* [ ] Contact the user indicating their initial password and steps to [#resetting-your-password](../../cdr-administration/santedb-administration-panel/managing-your-profile.md#resetting-your-password "mention")
* [ ] Contact the user's supervisor to indicate the account creation has been successful (alternately: resolve the help desk ticket to create a new user)

## Summary Information

**Current Status:** Example\
**Reviewed By:** SanteSuite Team

### **Revision History**

| Author                   | Date       | Changes         |
| ------------------------ | ---------- | --------------- |
| Justin Fyfe (SanteSuite) | 2022-01-08 | Initial Version |
|                          |            |                 |
|                          |            |                 |

### See Also

{% content-ref url="../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md" %}
[managing-user-accounts.md](../../cdr-administration/santedb-administration-panel/security-administration/managing-user-accounts.md)
{% endcontent-ref %}

{% content-ref url="../../cdr-administration/santedb-icdr-admin-console/user-administration.md" %}
[user-administration.md](../../cdr-administration/santedb-icdr-admin-console/user-administration.md)
{% endcontent-ref %}

