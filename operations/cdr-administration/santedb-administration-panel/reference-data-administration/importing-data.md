# Importing Data

{% hint style="info" %}
This page applies to SanteDB Version 3.0
{% endhint %}

## Import Dashboard

The import dashboard is accessed under the **Reference Data** menu in the **Import** screen.&#x20;

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

The dashboard shows the foreign data files which have been upload to the SanteDB server.

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

The status column indicates the state of the file:

* Completed Successfully- The import has been completed and no errors or issues were detected.
* Completed with Warnings - The import was partially completed, however there were issues with the source data.
* Rejected - The import was rejected - and cannot be imported.
* Staged - The import data is uploaded on the server, however it has not been scheduled for import
* Scheduled - The import data will be processed when the foreign data import job is next run.
* Running - The import data is currently being imported into the SanteDB database..

## Uploading an Import File

Imports for data are processed on the server in the background. To begin the process, access the upload screen and select the source file for import.

{% hint style="info" %}
Currently only CSV is supported as a data import format.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

1. Select the file which should be imported. Your file should be within the allowable file upload limit for your environment.
2. Select the import mapping which has been created by your development team. The **ONC Patient Matching Dataset** is included standard with SanteDB ([https://github.com/onc-healthit/patient-matching](https://github.com/onc-healthit/patient-matching))
3. Provide a friendly name for the import. This acts as the label for the import.

## Running the Import

After upload, the imports are placed into a **Staged** state. This state indicates that the file is valid and ready to be executed. The import process is executed by the **Import Foreign Data** background process, which is automatically run at midnight every night.&#x20;

The user can manually initiate the import process.

## Reviewing and Correcting Issues

After import, the file may be placed in the **Completed With Errors** state. This indicates that not all records could be processed in the file. Users can view the issues by clicking on the import details screen.

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

To correct import errors, you may download the **Rejected Records** file to your hard disk. This file matches the format of the original import file, with an additional column named `import_error`. This column indicates the issue that needs to be corrected.&#x20;

After all errors have been corrected, you may upload the corrected reject file, and repeat the process.
