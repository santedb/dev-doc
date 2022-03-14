# Managing Devices

In SanteDB, a security device represents an non-human security identity which is assumed by a device. Security devices in SanteDB are intended to represent physical devices (or nodes) which are accessing the SanteDB server.&#x20;

Devices have a secret (like an application) and may optionally have a public signing key registered with the SanteDB server.

## Device List

The device list is accessed using the `Devices` menu item in the security menu. The device list shows a list of all active (non-deleted) devices which are permitted to access the SanteDB iCDR instance.

![](<../../../../.gitbook/assets/image (432) (1) (1) (1) (1) (1).png>)

The actions which are available under this panel are:

* Create: Allows administrators to create a new device account
* Show Deleted: Allows administrators to view deleted accounts and optionally un-delete them.
* Edit: Change the properties of the device account
* Delete: Remove the device from the iCDR&#x20;
* Lock / Un-lock: Temporarily suspend the device security credential

{% hint style="info" %}
When locking or deleting a device account - no users or applications running on that device principal may access the SanteDB iCDR system.
{% endhint %}

### Device Self-Enrolment

The SanteDB dCDR service onboarding process well self-enrol the dCDR device with the central iCDR server (see: [installing-disconnected-gateway.md](../../../../installation/installation-1/deployment/software-deployment/disconnected-gateway/installing-disconnected-gateway.md "mention"), [installing-web-access-gateway.md](../../../../installation/installation-1/deployment/software-deployment/disconnected-gateway/installing-web-access-gateway.md "mention")).&#x20;

These enrolments can be disabled from the central iCDR device administration panel. When a dCDR device account is disabled, all synchronization and login activity from the web or disconnected gateway device are restricted.

## Creating a Device

To create a new security device click the `Create` button. Administrators may wish to manually create new devices when:

* A new HL7v2 trading partner is being setup&#x20;
* An new node-authentication partner account needs to be created (for Client Certificate Mapping)

![](<../../../../.gitbook/assets/image (440) (1) (1) (1).png>)

The `Name` of the device should be unique within the context of the SanteDB solution which has been deployed.&#x20;

The `Extended Properties` panel is used to capture non-security related information about the device. This information is affixed to `Act` events which&#x20;

| Model Name          | The name of the device model (used for inventory and validation).                                                                      |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Operating System    | Information about the operating system platform and version which the device is running.                                               |
| Designated Facility | If the device will be used in a single facility, this is the facility in which the device resides (useful for diagnostics and service) |
| Designated Person   | If the device is administered by another person, this field may track the official point of contact.                                   |

## Editing Devices

When editing a device, administrators will be shown the device security information. The `Core Properties` panel shows the provenance information (last update, creation, etc.) as well as the security ID (UUID for the object) and the name with which the device authenticates itself.

![](<../../../../.gitbook/assets/image (435) (1) (1) (1) (1) (1) (1).png>)

{% hint style="info" %}
The core properties of a security device cannot be edited once a device is created. It is recommended that administrators delete the device and re-add the device credentials.
{% endhint %}

### Security Properties

The security properties of the device are used for viewing lockout status, invalid authentication attempts and to change or view the device secret.

&#x20;

![](<../../../../.gitbook/assets/image (423) (1).png>)

#### Invalid Authentications

Whenever a device attempts to authenticate with this account, however uses incorrect credentials, this counter is increased. Invalid authentications can be reset using the `Reset` button on the user interface. This action will reset the invalid authentication attempts to 0.

#### Lockout

After a configured number of invalid authentication attempts, the device will automatically be locked out for a sliding window of time (the more invalid authentications the longer the lockout period). Additionally, administrators can manually lockout an account using the lock mechanism.&#x20;

A device account's lockout can be reset using the `Unlock` button.

#### Device Secret

The device secret allows an administrator to set a new device secret. The existing secret for the device is not shown (unless the device is new). Administrators can either `Edit` the secret to a custom value:

![](<../../../../.gitbook/assets/image (447) (1) (1) (1).png>)

After which, pressing the `Save` button will commit the change. Alternately the administrator can set the secret to a random value with `Reset`.

![](<../../../../.gitbook/assets/image (446) (1) (1) (1) (1).png>)

{% hint style="info" %}
When using X509 client certificate authentication, the secret of the device account should be X509 thumbprint of the certificate which the device will be presenting to the server. The value of the secret should be the `THUMBPRINT` attribute of the certificate in hexidecimal format in lower case. For example: `a11164321e30c84bd825ab20225421434622c52a`
{% endhint %}

## Assigning Policies

By default a new device will copy its policies from the `DEVICES` group. After creation policies can be customized using the policies panel. New policies are added by first searching for the policy and then pressing the `+` button.&#x20;

![](<../../../../.gitbook/assets/image (438) (1) (1) (1) (1) (1) (1) (1).png>)

By default a device will be assigned the policy with a GRANT permission. You can alter these by clicking the permission type.

![](<../../../../.gitbook/assets/image (433) (1) (1) (1) (1) (1) (1).png>)

The permission types in SanteDB are:

* Grant - The device will be granted access to any action or data carrying the policy
* Deny - The device is not permitted to access any action or data carrying the policy.
* Elevate - The device is, by default, DENY the request, and the server will send a authentication challenge back to the requestor. Users may be required to provide a reason for override and must provide their password.

Policies can be removed from a device by clicking the `Remove` button. When a policy is removed, it means that the device (or any application or using using it) has no specific grant applied to the policy (i.e. if the user is in a group its grant will apply, otherwise the default of DENY is applied).

