# Managing Applications

In SanteDB the a security application represents a piece of software code which is authorized to access data within the SanteDB iCDR environment. In OpenID nomenclature, an application in SanteDB represents an authenticated client (`client_id`/`client_secret`).

## Application List

The application list screen shows a listing of all registered security applications (and profiles) in the implementation of SanteDB.&#x20;

![](<../../../../.gitbook/assets/image (425) (1) (1).png>)

* Create Application Identity: Used to establish a new authenticated application.
* Details / Edit : Used to view the security details of the authenticated application and change if needed.
* Delete : Deactivates the application in the SanteDB server instance so no authentications or lookups will be resolved.
* Lock Application: Prevents the application or any user on that application from gaining access.

## Create Application

Creating a new application in the administrative portal establishes a new identity registration in the application identity provider. Data collected to create a new security application includes:

* Name: A unique name for the application in the SanteDB identity provider. The name is equivalent to the `client_id` in the oauth request.
* Software Name: A descriptive name of the software to which this application belongs.
* Software Vendor: A description of the software vendor/support contact&#x20;
* Software Version: The version of the software that owns this application credential

{% hint style="info" %}
If creating a security application for HL7 Version 2.x trading partners, the name of the application should be in format `MSH-4` format.
{% endhint %}

### Generate an Application Secret

Once created, the administrative interface will show the created application. The administrator must generate an application secret using the **Reset** option.

![](<../../../../.gitbook/assets/image (448) (1) (1) (1).png>)

The application secret should be saved and sent to the integration partner or application developer.

## Editing Applications

When editing an application from the application list or after creating an application, the properties of the device can be modified.

![](<../../../../.gitbook/assets/image (441) (1) (1) (1) (1).png>)

### Resetting Security State

Applications, like users and devices, can become locked if they fail to authenticate properly after a specified amount of time. This could be due to mis-configuration of the client or the security settings.&#x20;

Each time an application authentication attempt fails, the invalid authentication counter will be incremented until the application locks.&#x20;

![](<../../../../.gitbook/assets/image (443) (1) (1) (1) (1).png>)

An administrator the security settings:

1. Invalid Authentication attempts shows the number of the client application authentications that have failed. If the configured maximum authentication fails is exceeded by this counter the application account is locked.
2. Lockout shows the time until which time the application is locked. No authentication attempts will be permitted while the application is locked. (users may complain of applications not working or credentials not working). Unlocking the application will allow authentications with the credential.
3. Application secret allows for the changing of the application secret. The application secret is randomly generated, and should shared with the known development staff of the client application.

## Assigning Policies

By default a new application will copy its policies from the `APPLICATIONS` group. After creation policies can be customized using the policies panel. New policies are added by first searching for the policy and then pressing the `+` button.&#x20;

![](<../../../../.gitbook/assets/image (438) (1) (1) (1) (1) (1) (1).png>)

By default an application will be assigned the policy with a GRANT permission. You can alter these by clicking the permission type.

![](<../../../../.gitbook/assets/image (433) (1) (1) (1) (1) (1) (1).png>)

The permission types in SanteDB are:

* Grant - The application will be granted access to any action or data carrying the policy
* Deny - The application is not permitted to access any action or data carrying the policy.
* Elevate - The application is, by default, DENY the request, and the server will send a authentication challenge back to the requestor. Users may be required to provide a reason for override and must provide their password.

Policies can be removed from an application by clicking the `Remove` button. When a policy is removed, it means that the application (or any device or user using it) has no specific grant applied to the policy (i.e. if the user is in a group its grant will apply, otherwise the default of DENY is applied).
