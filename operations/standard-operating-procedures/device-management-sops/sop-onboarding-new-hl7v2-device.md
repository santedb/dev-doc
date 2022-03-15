# SOP: Onboarding new HL7v2 Device

## Summary

This procedure follows the correct procedures to follow when onboarding a new HL7v2 device on the SanteDB iCDR. The example here uses the procedures to setup a copy of OpenMRS 1.9.x running the [SanteDB Client Registry Module](https://github.com/santedb/openmrs-module-mpi-client) in HL7v2 mode (note: this procedure will be different based on the client software being configured)

### Use Procedure When

* [ ] Onboarding a new clinic using OpenMRS 1.9.x
* [ ] The iCDR is running with MSH-8 security mode over SLLP&#x20;

## Procedure

### Before Beginning

* [ ] Connected to the Internet
* [ ] Ensure the device is protected from threats
  * [ ] Device has the latest operating system installed
  * [ ] Device has its local firewall enabled and configured
  * [ ] Device has antivirus software and anti-malware software installed
* [ ] Ensure device name selected complies with the device naming conventions in the operational architecture documentation developed.
* [ ] Ensure that a most responsible person and/or facility has been documented for the device
* [ ] Ensure the users of the OpenMRS instance have received proper instructions on care and use of the device:
  * [ ] Reviewed and completed the Privacy Policy
  * [ ] Reviewed and completed the Acceptable Use Policy
  * [ ] Reviewed and completed the Data Sharing Process Documents

### Procedures / Tasks

1. Create the Device in the SanteDB administrative panel
   1. Access the SanteDB Administrative Portal by[logging-in.md](../../cdr-administration/santedb-administration-panel/logging-in.md "mention")
   2. Access the [security-administration](../../cdr-administration/santedb-administration-panel/security-administration/ "mention") menu item
   3. Access the [#device-list](../../cdr-administration/santedb-administration-panel/security-administration/managing-devices.md#device-list "mention") by clicking on the `Devices` link
   4. Press the `Create` button and enter the necessary details as documented in [#creating-a-device](../../cdr-administration/santedb-administration-panel/security-administration/managing-devices.md#creating-a-device "mention")
      1. Name of the device in HL7v2 format : `COMRS192|NAME_OF_FACILITY_DEVICE_ID` (note: `COMRS192` is the application registration for OpenMRS 1.9.2 and `NAME_OF_FACILITY_DEVICE_ID` should be the name of the facility in the standardized device format)
      2. Enter the Model Name of the server hardware (example: Lenovo ThinkCenter ST40)
      3. Enter the Operating System Name (example: Ubuntu Linux 20.04)
      4. Enter the MRP and/or facility where the device resides
   5. Press `Save`
   6. Generate a unique secret for the device by pressing `Reset` (see: [#device-secret](../../cdr-administration/santedb-administration-panel/security-administration/managing-devices.md#device-secret "mention"))
2. Setup the OpenMRS instance at the clinic
   1. Ensure that the MPI or SanteDB server is available from the clinic site (i.e. connected to internet)
   2. Install the OpenMRS MPI Client Module into the OpenMRS instance
   3. Click on the `Admin` page and then `Advanced Settings` in the OpenMRS instance
   4. Scroll to the relevant settings and use the following parameters:
      1. **mpi-client.endpoint.pdq.addr** : `mpi.example.com`
      2. **mpi-client.endpoint.pdq.port** : `2400`
      3. **mpi-client.endpoint.pix.addr** : `mpi.example.com`
      4. **mpi-client.endpoint.pix.port** : `2400`
      5. **mpi-client.endpoint.ar.addr** : `auditing.example.com`
      6. **mpi-client.endpoint.ar.transport** : `audit-tls`
      7. **mpi-client.endpoint.ar.port** : `11515`
      8. **mpi-client.security.authtoken** : `VALUE FROM STEP 1.6 ABOVE`+OMRS393\_#948
      9. **mpi-client.msg.sendingApplication** : `OMRS192`
      10. **mpi-client.msg.sendingFacility** : `NAME_OF_FACILITY_DEVICE_ID` (from 1.4.1 above)
      11. **mpi-client.msg.remoteApplication** : `EXAMPLE_COM_MPI`
      12. **mpi-client.msg.remoteFacility** : `DC_CENTRAL`
      13. **mpi-client.pid.exportIdentifierType** : `Patient ID=LOCAL_ID,National ID=NAT_HEALTH_ID`
      14. **mpi-client.pid.defaultCountry** : `ELBONIA`
      15. **mpi-client.pid.enterprise** : `MPI_KEY_UUID`
      16. **mpi-client.pid.local** : `NAME_OF_FACILITY_DEVICE_ID`
      17. **mpi-client.pid.nhid** : `NAT_HEALTH_ID`
      18. **mpi-client.pid.updateIdTypes** : `false`
   5. Press the `Save`button
   6. Visit the `Search MPI Patient` link in the header and enter the search query `TEST_VALIDATE`  - a single patient result should be returned

### After Completion

* [ ] Review the OpenMRS business processes developed as part of the deployment of the MPI
* [ ] Document the deployment (or close opened tickets for installation)&#x20;

## Summary Information

**Current Status:** Example\
**Reviewed By:** SanteSuite Team

### **Revision History**

| Author                   | Date       | Changes         |
| ------------------------ | ---------- | --------------- |
| Justin Fyfe (SanteSuite) | 2022-03-15 | Initial Version |
|                          |            |                 |
|                          |            |                 |

###
