# Logging In

Upon navigating to the SanteDB iCDR administration panel for your deployment, the administration portal will challenge you for a login. The components of the login screen are illustrated below.

![](<../../../.gitbook/assets/image (423) (1) (1) (1).png>)



* **Username Input**: This is a the security name which was created for your user. On a default installation of SanteDB the administrator account is `Administrator`. User names are case-insensitive, meaning `AdMiNiStRaToR` is equivalent to `administrator`.
* **Password Input:** This is the password which was provided to you by your administrator. The default password for a SanteDB installation is `Mohawk123`.
* **Login:** This button submits the authentication credentials you've entered to the identity provider and establishes a session for your account.
* **Forgot Password**: This button initiates a password reset operation.

## Forgot Password

To initiate the password reset workflow, click the `Forgot Password` button, this will open a new dialog which will permit the entry of a username.

![](<../../../.gitbook/assets/image (427) (1) (1) (1) (1) (1) (1).png>)

Next, enter the answer to the provided security challenge question.

![](<../../../.gitbook/assets/image (436) (1) (1) (1) (1) (1).png>)

Finally, enter the new password for your user account, the password should adhere to the jurisdictions password complexity and history requirements.

![](<../../../.gitbook/assets/image (437) (1) (1) (1) (1) (1) (1) (1) (1).png>)

{% hint style="info" %}
Your jurisdiction may have enabled SMS or e-mail password reset mechanisms. If this is the case, you will receive an e-mail link or SMS code with a one time password for password reset.
{% endhint %}

