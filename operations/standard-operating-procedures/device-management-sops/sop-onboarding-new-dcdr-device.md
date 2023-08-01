# SOP: Onboarding new dCDR Device

## Summary

SanteDB's dCDR software support self-service registration of dCDR instances provided the user self-enrolling the device has proper permissions (**Create Device**). The self-service procedure will vary depending on:

* The dCDR plugins and customizations performed (i.e. the MEMPI RegApp is different than TImR App self-service enrolment)
* The strategy for the dCDR instance (online or synchronized)
* The subscription architecture of the dCDR instances (identifier, catchment, etc.)

### Use Procedure When

* [ ] A new device is being setup with an app that is built on the dCDR technology (Android application, Web Access Gateway, Disconnected Gateway, etc.)
* [ ] The device has not previously been setup or configured on the iCDR interface&#x20;

## Procedure

### Before Beginning

* [ ] Connected to the Internet
* [ ] Ensure the device is protected from threats
  * [ ] Ensure the device has the latest operating system installed
  * [ ] Ensure the device has its local firewall enabled and configured
  * [ ] Ensure the device has antivirus software and anti-malware software installed
* [ ] Ensure device name selected complies with the device naming conventions in the operational architecture documentation developed.
* [ ] Ensure that a most responsible person and/or facility has been documented for the device
* [ ] Install the appropriate dCDR software on the device
* [ ] Ensure the user of the device has received proper instructions on care and use of the device:
  * [ ] Reviewed and completed the Privacy Policy
  * [ ] Reviewed and completed the Acceptable Use Policy
  * [ ] Reviewed and completed the Data Sharing Process Documents

### Procedures / Tasks

1. When the dCDR interface opens with the initial configuration screen enter the onboarding information:
   1. Device name following the established naming conventions
   2. Use mysantedb.example.com as the realm
   3. Modify the client secret information to match the modified client secret sent to you (should be in the operational documentation)
   4. Ensure Use TLS is selected
   5. Join the domain
2. Follow the onboarding procedure documented in [disconnected-gateway](../../../installation/installation-1/deployment/installing-software/disconnected-gateway/ "mention")
   1. If installing a web-access gateway follow the online setup procedures documented in [#configure-the-web-access-gateway](../../../installation/installation-1/deployment/installing-software/disconnected-gateway/installing-web-access-gateway.md#configure-the-web-access-gateway "mention")
   2. If installing on a disconnected mode follow the offline setup procedures documented in [#configuration](../../../installation/installation-1/deployment/installing-software/disconnected-gateway/installing-disconnected-gateway.md#configuration "mention")
3. When prompted to select an optimization strategy select the slowest network speed (highest compression rate - 2g/Dial Up)
4. Allow the initial synchronization to complete (there should be a notification that initial synchronization is complete)

### After Completion

* [ ] Update the facility and most responsible person (if applicable) in the administrative panel (see:  [managing-devices.md](../../cdr-administration/santedb-administration-panel/security-administration/managing-devices.md "mention"))
* [ ] Update the device information including Operating System, Manufacturer, Model (if required) in the administrative panel
* [ ] Provide the device to the primary user and close the ticket

## Summary Information

**Current Status:** Example\
**Reviewed By:** SanteSuite Team

### **Revision History**

<table><thead><tr><th width="150">Author</th><th width="245">Date</th><th>Changes</th></tr></thead><tbody><tr><td>Justin Fyfe (SanteSuite)</td><td>2022-03-15</td><td>Initial Version</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

