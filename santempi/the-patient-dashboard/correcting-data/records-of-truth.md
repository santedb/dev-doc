# Records of Truth

When you edit a record which has been identified as a master record, you are actually editing what is known as a "Record of Truth". The record which was sent from the source system is left as it was collected/sent to the MPI.&#x20;

For example, if two clinics have sent records which have been linked together by the matching algorithm, the logical relation of these elements would be as illustrated below:

![](<../../../.gitbook/assets/image (23).png>)

Within the tool's **Master Data Management** tab you will see both locals listed.

![](<../../../.gitbook/assets/image (117).png>)

When you start editing a master record, you're establishing a record of truth for that record. You will be warned of this fact when editing the patient.

![](<../../../.gitbook/assets/image (75).png>)

After saving the changes you've made, the SanteMPI backend will establish a new Record of Truth. Logically this appears in the SanteDB CDR as:

![](<../../../.gitbook/assets/image (137).png>)

In the **Master Data Management** tab of the patient view this record will be indicated as the record of truth.

![](<../../../.gitbook/assets/image (8).png>)

Records of Truth also appear in the **Entity Relationships** diagram for the record as a Record of Truth.

![](<../../../.gitbook/assets/image (103) (1).png>)

Subsequent edits to the patient will result in edits to the record of truth. This fact will be indicated with an informational alert on editing.

![](<../../../.gitbook/assets/image (2).png>)
