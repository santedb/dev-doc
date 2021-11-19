# SanteDB Administration Panel

When the instance of SanteDB iCDR was installed in your environment, the Administration User Interface may have been installed. The administrative user interface is a specialized form of the SanteDB dCDR which services web-based requests.

{% hint style="info" %}
You may use the [Demonstration Server's](../../../santedb/demonstration-environment.md) administration panel as a reference for this document.
{% endhint %}

## Table of Contents

* [Logging In](logging-in/)
* [Managing your User Profile](managing-your-profile.md)
* [Security Administration](security-administration/)
  * [Managing User Accounts](security-administration/managing-user-accounts.md)
  * Managing Application Roles&#x20;
  * Managing Device Accounts
  * Managing Application Accounts
  * Managing Application Security Policies
  * Reviewing Audit Log Events
* Application Administration
  * Gathering and Reviewing Log Files
  * Running and Maintaining System Jobs
  * Enabling and Collecting Bug Reports
* Reference Data Administration
  * Identity Domain Management
  * Place Management
  * Facilities Management

## Dashboard

When you log into the SanteDB Administration Panel user interface, the default screen is the server dashboard. Depending on the plugins you have enabled (SanteMPI, SanteIMS, etc.) and your level of user access (clinical data, administrative data, etc.) you will see a series of summary dashboards for your account.

![](<../../../.gitbook/assets/image (431).png>)

* System Menu: The system menu provides a series of links to administrative screens which your user account can access.&#x20;
* Dashboard Area: The dashboard area of your administrative panel. This will change depending on your jurisdiction, plugins installed, and user access.
* Connection Mode: For the administrative panel this will display `Direct Connect to Server`. If you're operating a disconnected client instance this badge will not appear.
* System Mail Messages: If using SanteDB offline or leveraging system alert mail, this is the system mailbox.
* System Alerts: Any tickles (notifications) that are raised which require your attention will be placed in the system alert area.
* Connection Status: If administering a disconnected instance of the SanteDB dCDR this indicates the connectivity of the dCDR with the iCDR server.
* User Menu: This allows you to logout of your session and to also [Manage Your Profile](managing-your-profile.md).

### SanteMPI Dashboard

By default, the SanteMPI dashboard shows a summary of MPI information for any authenticated user which has `Query Clinical Data` policy enabled.

![](<../../../.gitbook/assets/image (439).png>)

* Recent Patients: The recent patients widget on the dashboard shows a list of all patients which have been registered on the iCDR or dCDR in the last 24 hours.
* Quick Search: Allows for a query free-field search by name, address, or identifier. Additionally, devices with a camera can use the SanteDB Visual Resource Pointer QR code to directly open a patient profile.
* Patient Population Statistics: Shows a quick summary of all patients registered in the system by gender and by age distribution.
* System Activity: Shows a trend of system activity (driven by audit traffic) for the solution.
