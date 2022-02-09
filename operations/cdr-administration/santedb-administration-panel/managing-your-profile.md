# Managing Your Profile

SanteDB's administration panel provides user self-service operations which allow any user to self-administer their profile. The profile administration screen is accessed by clicking on the user name on the top right side of your browser window.

![](<../../../.gitbook/assets/image (432) (1) (1) (1) (1) (1) (1).png>)

After visiting this page, the user profile screen will be displayed. SanteDB's security subsystem separates user information into two components:

* Security Profile: This is used for authentication, security event reporting, password management, and multi-factor information.
* User Profile: This is your publicly shown user profile which is shown on clinical events (like registrations, clinical acts, etc.).&#x20;

The difference between the two is your security profile is only shared when you log into a remote system, whereas your clinical or user profile is synchronized and downloaded/shared with other systems.

![](<../../../.gitbook/assets/image (417).png>)

## Profile

By clicking on the pencil icon in the `Profile` panel, you will enter `Edit` mode. Here you can update your personal user profile for the solution.

![](<../../../.gitbook/assets/image (435) (1) (1) (1) (1) (1) (1).png>)

You can edit the following information on the tabs provided:

* Name: The first, last, prefix and suffix portions of your name.
* Address: Your mailing, home or workplace address.
* Contact Info: Public contact addresses (e-mails or telephone numbers) where users can contact you to clarify records data issues.
* Additional Information:
  * Your Gender (if you prefer to share it)
  * Your Birth Date
  * Your Assigned Facility (the facility you are the administrator of)
  * Your Employer
  * Your Preferred Language

{% hint style="info" %}
Setting your preferred language will change the user interface language when you log into any SanteDB dCDR instance.
{% endhint %}

## Security Profile

The security profile panel allows you to modify your security settings for SanteDB.

![](<../../../.gitbook/assets/image (428) (1) (1) (1) (1) (1) (1).png>)

* Last Login: Shows the last time that you logged into the SanteDB iCDR server
* Security E-Mail: The e-mail address where you would like to receive password reset codes, or TFA codes.
* Security Phone: The telephone number where you would like to receive password reset codes, or TFA codes.
* TFA Enabled: If your jurisdiction has setup the necessary infrastructure, you can enable two-factor authentication. This means that you will receive an e-mail or SMS code whenever you log in which contains a one-time password.
* Password Recovery: One or more password recovery questions which can be used to [Reset Your Password](logging-in.md#forgot-password).
* Password: The expiration time of your password, and the option to reset your password.

### Resetting your Password

If you would like to reset your password, you can click the `Reset Pwd` button , this will open a new dialog which will allow you to enter your existing password and a new password.

![](<../../../.gitbook/assets/image (433) (1) (1) (1) (1) (1) (1) (1).png>)



