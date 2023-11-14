# Managing User Accounts

Active management of user accounts is paramount to the security of SanteDB servers. As discussed in the Security Architecture article, SanteDB authenticates users, devices and applications, each which are combined to a principal or session.

User accounts are used to link to **Humans that use SanteDB**.&#x20;

{% hint style="info" %}
It is best practice to keep user accounts as **Human Users** which are using the SanteDB system in an interactive capacity or **System Users** which are internal to the host process. If you wish to implement service or non-human users which need to interact with SanteDB it is recommended you use **Device** and **Application** credentials instead.
{% endhint %}

## User List

The summary screen provides a comprehensive list of all users found in the SanteDB solution. This user list is scoped to the system on which the panel is running (i.e if you're accessing the panel from a disconnected client, these are the local users which can access the dCDR, if you're accessing the panel on an iCDR these are all users).

![](<../../../../.gitbook/assets/image (41).png>)

You can sort/order the table by any field which has a sort indicator, additionally each row of the user list performs actions on each user on the same row.

![](<../../../../.gitbook/assets/image (534).png>)

* Edit: Opens the detailed user information screen
* Delete: Indicates that the user account is no longer active (i.e. the employee is fired, moved departments, etc.)
* &#x20;Lock/Unlock: Activates a user lockout - this prevents the user account from logging into the SanteDB server.
* Reset Pwd: Allows for an administrative reset of the user's password.

### Deleted Users

It is best practice to lock user accounts when you are investigating a security breach, or suspect an account may be compromised. However, there are occasions when you wish to remove a user from the active users list (such as termination of employment, change of role, etc.).

When you delete a user they are marked as inactive. You can access these accounts by using the `Show Deleted` option in the user interface. Deleted user accounts provide an option to restore or un-delete the account (as well as edit the information).

![](<../../../../.gitbook/assets/image (502).png>)

## Creating User Accounts

When you press the `Create` button on the user summary screen, you will be provided an opportunity to create a new user account.&#x20;

{% hint style="info" %}
This article explains the mechanics of creating a new user. Please refer to the Standard Operating Procedure for more information about the business process surrounding this screen.
{% endhint %}

![](<../../../../.gitbook/assets/image (625).png>)

* Username: Enter a unique user name for the specific user which will be using the system. It is best practices that this map to a single, individual user account.
* Role: Select one or more roles for the user account. Built-in roles are generally:
  * `CLINICAL_STAFF` - Users which need access to clinical data, and not administrative data (except to manage their local clinic)
  * `ADMINISTRATORS` - Users which need access to administrative functions, however do not need access to clinical data.
  * `USERS` - Users which are general in nature - these users can login however cannot access clinical data nor administrative data.
* Password: The initial password to set for the new user.&#x20;
* Security E-Mail: The e-mail address where the user's welcome package should be e-mailed (if configured) or where TFA alerts should be sent.
* Security Phone: The phone number where user's TFA data should be sent.
* Preferred Language: The language which the user will use to access the user interface (apps, or other data controlled by SanteDB)
* Primary Facility: If you're using the dCDR and mobile applications, this is the facility where the user is assigned.&#x20;
* Employer: The organization which employs the user, this is used for contacting the employer to verify employment status.

## User Details

When you use the `Edit` option to view the details of a user, you will be presented with the user information detail screen.&#x20;

![](<../../../../.gitbook/assets/image (319).png>)

* Security Tab: The security tab is used to edit the core security attributes of the user. This includes:
  * Resetting the user's password
  * Resetting user's password
  * Setting the user's TFA settings
  * Changing security settings (e-mail, phone number).
* Profile Tab: The profile tab is used to control the user's public profile such as name, date of birth, etc.
* Activity Tab: The activity tab shows the activity in the system which was initiated by the user which is being viewed. This data allows administrators to see what the user has been doing in the SanteDB system.
* Audit Trail: The audit trail tab shows the data in the audit trail for the user account itself. This tab differs from the activity tab in that the activity tab shows actions initiated BY the user, the audit trail tab shows the actions performed AGAINST the user.

### Editing Security Settings

Clicking on the pencil on the security properties panel will enable the editing of the user's security settings. When complete, clicking the check button to commit your changes.

![](<../../../../.gitbook/assets/image (618).png>)

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


![](<../../../../.gitbook/assets/image (600).png>)





