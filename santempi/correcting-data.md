# Correcting Data

{% hint style="info" %}
The MPI is intended to keep records of truth, and therefore editing details of patients sourced from other systems is only recommended when establishing a record of truth, or running in a simple deployment.
{% endhint %}

## Editing in Multi Instance Mode on iCDR

To edit a patient record on the master iCDR server, you can simply press the pencil \(edit\) icon on the panel whose information you'd like to edit. 

![](../.gitbook/assets/image%20%2819%29.png)

This will change the view of the panel into an edit mode, which allows administrative editing of the record.

![](../.gitbook/assets/image%20%2876%29.png)

{% hint style="info" %}
As indicated on the edit view, editing a master record will establish a "RECORD OF TRUTH" for that object. Administrative edits should only be done in the MPI when confirmed data for the patient has been obtained \(for example: through a formal registration process or in-person identification at a registration centre\).
{% endhint %}

Clicking on the name tab reveals that there are multiple names for which the patient has been registered. 

![](../.gitbook/assets/image%20%2845%29.png)

Here the user has selected the person's official name for recordkeeping purposes is Thomaso Tom Thomson \(the user is keeping the search names so the patient will continue to show up in search results with their other names\). 

![](../.gitbook/assets/image%20%2884%29.png)

{% hint style="info" %}
Depending on your configuration of SanteMPI, you may see additional fields for name prefix, family name, suffix, etc. This particular view has been configured in a context where family names and prefix/suffix information is not used and name tokenization has been enabled.
{% endhint %}

The user may also establish an official information for the record, any data which has been matched from local records is pre-populated where possible. 

![](../.gitbook/assets/image%20%2868%29.png)

When complete pressing the check button on the title bar will submit your changes.

![](../.gitbook/assets/image%20%2824%29.png)

Once the record is submitted, refreshing the record will indicate the changes have taken place, this is indicated by a gavel icon appearing the in the patient header.

![](../.gitbook/assets/image%20%289%29.png)

Additionally, this record will appear as the record of truth in the entity relationship diagram.

![](../.gitbook/assets/image%20%2858%29.png)

The record of truth is also indicated on the master data management widget tab \(if installed\) and is indicated in the list with a gavel.

![](../.gitbook/assets/image%20%2864%29.png)

{% hint style="info" %}
When performing matches the record of truth data is used for classification, blocking will use local records to provide maximum coverage of potential matches.

Additionally, when searching any of the child record information can continue to be used, and on all standards based interfaces \(HL7, FHIR, etc.\) the record will be disclosed as the ROT unless the caller specifically requests a copy of the local record \(for example, by using identifier\).
{% endhint %}

## Editing in Single Instance Mode or dCDR

When you edit a record in single instance mode, or when you're editing a patient on a local dCDR \(which does not support MDM\) you can edit a record just as you would normally on the iCDR, however you will be presented with a warning editing a LOCAL record.

![](../.gitbook/assets/image%20%2829%29.png)

If you edit a record in the dCDR which was sourced from another system \(like a local copy of OpenMRS or another HL7 ADT or FHIR feed\) you will overwrite the data in the dCDR for that patient and you can potentially create a data mismatch between the source and the dCDR.

When the record is synchronized to the master server, however, the iCDR will only update the local record for the dCDR record. The iCDR will no longer have visibility into the data that was submitted by the source system in the clinic.

![](../.gitbook/assets/image%20%2882%29.png)

