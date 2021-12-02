# Local Records

You are considering to be editing a local record when:&#x20;

* The iCDR is running in simple , single instance mode
* You're editing the patient on the dCDR
* You're manually editing a LOCAL record on the iCDR

{% hint style="info" %}
Editing LOCAL records on the iCDR which is running with Master Data Management enabled is **NOT RECOMMENDED**. Any corrections to local records should be performed on the source system which was responsible for the creation of the local record.
{% endhint %}

When you edit a local record, you will be presented with a warning editing a LOCAL record.

![](<../../.gitbook/assets/image (81).png>)

If you edit a record in the dCDR which was sourced from another system (like a local copy of OpenMRS or another HL7 ADT or FHIR feed) you will overwrite the data in the dCDR for that patient and you can potentially create a data mismatch between the source and the dCDR.

When the record is synchronized to the master server, however, the iCDR will only update the local record for the dCDR record. The iCDR will no longer have visibility into the data that was submitted by the source system in the clinic.

![](<../../.gitbook/assets/image (82).png>)
