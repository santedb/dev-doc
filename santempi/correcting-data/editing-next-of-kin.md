# Editing Next of Kin

{% hint style="info" %}
Next of Kin \(or Family Members\) are linked entities to the patient. When you edit the information for a family member within the patient view, you're actually editing information on another record. This may result in a shared update if the target family member is strongly linked between entities.
{% endhint %}

A patient's next of kin is displayed in the **Next of Kin** panel and can be edited by clicking the **pencil** icon.

![](../../.gitbook/assets/image%20%28126%29.png)

### Patients as Family Members of Patients

When a strong record exists \(i.e. a patient's family member has been promoted to a proper Patient type in SanteDB\), you will not be permitted to edit the record inline \(as this would cause an update without proper context\). You'll first need to visit the local record for the target of the link.

This can be done by clicking the **View** action when instructed, and editing the details of the family member on the Patient demographics page.

![](../../.gitbook/assets/image%20%2876%29.png)

### Person Family Members

Editing a patient's family members when linked to a person \(not a patient\) is done inline, the tabs for this edit process is the same as [Editing Demographic Information](editing-demographic-information.md) for patients.

![](../../.gitbook/assets/image%20%2849%29.png)

### Converting a Person to Patient

There are use cases where a family member should be upgraded from a Person reference to a Patient reference. This process happens:

1. Automatically when an HL7 ADT message is received containing a known identifier for the family member \(automatic conversion from Person to Patient\), or
2. Manually, when an administrator converts the patient.

The reason for this conversion is:

* You might want to take advantage of MDM functionalities not available to related persons
* You want to indicate that the family member is receiving care, however don't want to re-key the information

Manual conversion is a two-step process. Start by clicking the **Convert** option in the edit window

![](../../.gitbook/assets/image%20%28132%29.png)

Complete the **Birth** information tab that appears when selecting this option. Complete the suspected DOB for the patient and gender. Once complete, press **Convert** again to complete the process.

![](../../.gitbook/assets/image%20%2880%29.png)

You will note that the edit screen now instructs you to view the detail page for the newly created patient. Doing so will open the newly created patient record for that family member.

![](../../.gitbook/assets/image%20%28136%29.png)





