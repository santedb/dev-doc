# Records of Truth

When you edit a record which has been identified as a master record, you are actually editing what is known as a "Record of Truth". The record which was sent from the source system is left as it was collected/sent to the MPI.&#x20;

For example, if two clinics have sent records which have been linked together by the matching algorithm, the logical relation of these elements would be as illustrated below:

![](<../../.gitbook/assets/image (23).png>)

Within the tool's [master-data-management-tab.md](../../user-guides/santempi/the-patient-dashboard/master-data-management-tab.md "mention") **** tab you will see both locals listed.

![](<../../.gitbook/assets/image (428).png>)

Whenever an administrator uses the administrative panel to edit this record, it does not alter the data within the record, rather it establishes a record of truth. In the CDR this type of data can be thought of as:

![](<../../.gitbook/assets/image (137).png>)

In the **Master Data Management** tab of the patient view this record will be indicated as the record of truth with a gavel icon.

![](<../../.gitbook/assets/image (432).png>)

Whenever a record has a record of truth associated with it, the user interface and MPI will redirect all administrative panel updates from the MASTER to the record of truth (as indicated on the header).

![](<../../.gitbook/assets/image (434) (1).png>)

Records of truth are used by the SanteMPI system to determine what data is returned in queries and fetches of the master record. This type of functionality can be used to establish a curated **Golden Record** for the patient with official data.

Updates performed against this record are not permitted unless the sending credential has appropriate permission to edit/change the official information for the patient.
