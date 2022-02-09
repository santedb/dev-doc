# Seeding ONC Patient Matching Data

Once a docker image is setup - it can now be seeded or populated with data. In addition to running the installation qualification tool, you can seed the ONC dataset into the SanteMPI server which has just been setup.&#x20;

{% hint style="info" %}
It is recommended seeding the entire ONC dataset be done on a host machine with at least 8 GB of RAM, 4 CPU cores, and an SSD
{% endhint %}

## Download Resources

In order to complete this tutorial you will require the following tools:

* A setup version of SanteMPI (you can use the [.](./ "mention"))
* The ONC Patient Matching Challenge Data ([https://github.com/onc-healthit/patient-matching](https://github.com/onc-healthit/patient-matching))
* The SanteDB SDK (you can see [installation](../installation/ "mention"))

## Prepare SanteMPI for ONC Data

First, we're going to need to prepare our SanteDB server to accept the ONC data, this includes:

* Creating the necessary identity domains for the ONC spreadsheets
* Setting the matching configuration appropriately&#x20;

### Creating Identity Domains

The ONC dataset has two identity domains which need to be created in the SanteDB server. To do this, log into the administrative portal and click on **Reference Data** then **Identity Domains** and press **Create**.

You will need to register two identity domains:

| Namespace | URL                | OID              | Unique |
| --------- | ------------------ | ---------------- | ------ |
| ONC       | http://onc.org/eid | 2.25.4949384934  | true   |
| MRN       | http://onc.org/mrn | 2.25.17237262721 | false  |

### Optimizing Match Configuration

The ONC dataset is a large dataset where the source records (provided in the CSV files) can reliably represent a patient, because of this we can get an added performance bonus by changing our match configuration to source/source mode rather than source/master (since there is nothing that a master record would add in blocking).

To change the match configuration, click on **SanteMPI** then **Match Settings** locate the `org.santedb.matching.patient.default` entry and click **View.**

On the **Blocking** tab if we expand a blocking instruction we see the default method of matching is Source/Master:

![](<../../.gitbook/assets/image (432) (1).png>)

We can change this by pressing **Edit** (pencil) and modifying both blocking instructions. After this step the configuration should appear as:

![](<../../.gitbook/assets/image (449) (1).png>)

## Prepare ONC Dataset

Now that our MPI is setup correctly we should navigate to the directory where the ONC patient source data was cloned. To seed the data more easily, create a new batch file (if on Windows - if on Unix you should create an equivalent shell file) to call the SDK:

{% code title="seed-onc.bat" %}
```batch
@echo off
for %%F in (*.csv) do (
	start "Seeding %%F" "c:\Program Files\SanteSuite\SanteDB\SDK\importer.exe" --realm=http://127.0.0.1:8080 --user=Allison --password=Mohawk123 --source="%%F" --dataset=ONC --eid=ONC --mrn=MRN --ssn=SSN
)batch
```
{% endcode %}

The batch file will look at all the CSV files in the current directory and for each one it will:

* Start a new process
* Call the importer from the SDK with
  * The CSV file to be seeded
  * The realm on the local computer
  * Logged in as "Allison" and "Mohawk123" as password (i.e. this is Allison sending the data to the MPI)
  * Source format is ONC (opposed to FEBRL)
  * Enterprise ID is the ONC domain
  * Medical Record Number field maps to MRN domain
  * Social Security Number field maps to SSN domain

Now you can open a command prompt and type `seed-onc.bat` to start the seeding process. There will 9 consoles opened and 9 clients will begin seeding data to the MPI.

![](<../../.gitbook/assets/image (443) (1).png>)

The overall health of your deployment can be monitored on the Probes page.

![](<../../.gitbook/assets/image (437) (1).png>)
