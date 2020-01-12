# User Management

The administrative portal provides several key functions related to the administration of users. 

## Reviewing User Accounts

To review user accounts, you can select the Security &gt; Users option in the administration panel.

![](../../../.gitbook/assets/image%20%282%29.png)

From this screen you can quickly:

* Lock or unlock a user account which has been compromised
* Reset a password for a user
* Delete or un-delete a user account.

## Creating / Editing User Accounts

To create a new user account, press the **Create** button, to edit an existing user account, press the **Edit** button beside the user you'd like to edit. You'll be presented with a user creation screen as illustrated below.

![](../../../.gitbook/assets/image%20%2862%29.png)

The user edit / creation screen is broken into four sections:

* **Core Properties:** Which contains the core properties of the user account \(creation/updated user, security ID, username, etc.\)
* **Security Properties:** Role membership, invalid login tracking, and password control.
* **Demographic Fields:** Demographics related to the user who owns the account \(name, organization, facility, etc.\)
* **Version Information:** Complete changelog of edits made to the user account.

### Demographics Fields

![](../../../.gitbook/assets/image%20%2838%29.png)

Users in SanteDB have to profiles. The first profile is the **SecurityUser**, which are the attributes that the user uses for security reasons. The second profile is their **UserEntity** profile \(and optionally **Provider** profile\), which is a clinical representation of the user. 

To imagine the difference, you can think of an e-mail address or telephone number attached to security user as being the address used by the system for things like TFA and password resets, however the e-mail on the clinical profile may be for clinical purposes like booking appointments, referrals, etc.

### Version History

All clinical data \(including Provider and UserEntity data\) is versioned in SanteDB. This section of the screen shows a complete edit history of the clinical data, including which fields were changed, which user changed the fields, and which device/application was used to change the data.

![](../../../.gitbook/assets/image%20%289%29.png)

