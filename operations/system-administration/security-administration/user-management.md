# User Management

The administrative portal provides several key functions related to the administration of users. To see the counterpart to these functions from the perspective of the [SanteDB iCDR Admin Console](../host-administration/santedb-icdr-admin-console/), see the [User Administration](../host-administration/santedb-icdr-admin-console/user-administration.md) page.

## Reviewing User Accounts

To review user accounts, you can select the Security > Users option in the administration panel.

![](<../../../.gitbook/assets/image (9).png>)

From this screen you can quickly:

* Lock or unlock a user account which has been compromised
* Reset a password for a user
* Delete or un-delete a user account.

## Creating User Accounts

To create a new user account, press the **Create** button. You'll be presented with a user creation screen as illustrated below.

![](<../../../.gitbook/assets/image (125).png>)

The user edit / creation screen is broken into four sections:

* **Core Properties:** Which contains the core properties of the user account (creation/updated user, security ID, username, etc.)
* **Security Properties:** Role membership, invalid login tracking, and password control.
* **Demographic Fields:** Demographics related to the user who owns the account (name, organization, facility, etc.)
* **Version Information:** Complete changelog of edits made to the user account.

### Demographics Fields

![](<../../../.gitbook/assets/image (81).png>)

Users in SanteDB have to profiles. The first profile is the **SecurityUser**, which are the attributes that the user uses for security reasons. The second profile is their **UserEntity** profile (and optionally **Provider** profile), which is a clinical representation of the user.&#x20;

To imagine the difference, you can think of an e-mail address or telephone number attached to security user as being the address used by the system for things like TFA and password resets, however the e-mail on the clinical profile may be for clinical purposes like booking appointments, referrals, etc.

## Editing Users

To edit a user, click the **Edit** button beside the user that you wish to edit. You will be presented with a screen as illustrated below.

![](<../../../.gitbook/assets/image (7).png>)

### Editing Security Settings

Clicking on the pencil on the security properties panel will enable the editing of the user's security settings. When complete, clicking the check button to commit your changes.

![](<../../../.gitbook/assets/image (140).png>)

{% hint style="info" %}
The e-mail and phone number information on the security properties panel is only used for security purposes (like TFA, password resets, etc.). If you're using SanteDB with a third party IdP, Active Directory or LDAP authentication these fields will attempt to update the profile on the source system. This differs from the clinical contact information on the profile tab which is always stored in SanteDB.&#x20;
{% endhint %}

### Editing User Profile

SanteDB security users also have a profile exposed in the CDR (apart from the security tables) which contain information such as:

* Name
* Employment
* Assigned Places of Work
* Business Contacts
* Addresses

These can be edited using the **profile** tab of the user's detail screen.\


![](<../../../.gitbook/assets/image (39).png>)
