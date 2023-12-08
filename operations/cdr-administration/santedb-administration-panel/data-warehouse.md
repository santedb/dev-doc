# Data Warehouse

{% hint style="info" %}
This page describes a feature in SanteDB 3.0
{% endhint %}

SanteDB 3.0 added the ability for developers and system implementers to specify [Data Warehouse and Data Marts](../../../developers/applets/business-intelligence-bi-assets/bi-asset-definitions/data-marts.md) in their applet definition file. When an applet containing a data mart definition is loaded and installed into the SanteDB data mart definition manager.

Administrators may wish to selectively enable and/or disable the data warehouses and marts that these definitions create. This process is managed through the **Business Intelligence** section of the SanteDB administrative portal.

<figure><img src="../../../.gitbook/assets/image (467).png" alt=""><figcaption></figcaption></figure>

When an administrator accesses this management screen, they are presented with a master list of all data mart and warehouse definitions in their installed copy of SanteDB.&#x20;

<figure><img src="../../../.gitbook/assets/image (468).png" alt=""><figcaption></figcaption></figure>

The index screen enumerates the available data mart definitions and shows:

* Datamart - The logical name of the datamart which can be used to derive new datamarts.
* Description - The documentation for the datamart as provided by the developer
* Status - Shows the current status of the data mart
  * Not Registered - The datamart definition is installed, however the ETL jobs and database it defines are not being populated.
  * Running - The datamart definition is currently refreshing the data in the data mart it defines
  * Success - The datamart is up to date as of the last execution of the ETL job
  * Failure - The datamart could not be refreshed or is partially refreshed

Actions which can be taken on a datamart definition are:

* Register - Instructs the SanteDB server that the contents of the datamart should be registered. This process will:
  * Create the datamart database and data source in the BI layer
  * Migrate all the tables and schema definitions
  * Run the initial ETL process for population of the data mart.
* View - Opens the datamart detail
* Un-Register- Instructs the SanteDB server that the contents of the datamart should be removed from the database server. This process will:
  * Un-register the datasource from the BI layer
  * Drop the database (in PostgreSQL) or delete the database file (SQLite)

## View Data Mart

Details about a registered data mart can be obtained by clicking on the **view** option in the list of warehouse data marts.

<figure><img src="../../../.gitbook/assets/image (472).png" alt=""><figcaption></figcaption></figure>

### Datamart Refresh Executions

The main screen of the data mart shows the list of execution runs that have been performed on the mart. By default, SanteDB will refresh all registered data marts using the **Refresh Datamarts** job. This list provides an enumeration of each time that the data mart has been refreshed.&#x20;

Details about the refreshing of a data mart can be obtained, and shows a summation of the data mart execution and the overall result along with diagnostic details of the data mart.

<figure><img src="../../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
The execution of data-mart refresh operations are performed using database specific SQL commands. Errors should be diagnosed by a database administrator (DBA) who cares for the installation of the software.
{% endhint %}

### Datamart Schema

As described above, the purpose of a data-mart is to pre-compute data for reporting and analysis outside of SanteDB. These operations can include:

* Pivoting normalized data into a de-normalized form which is easier for report writing and analysis
* Pre-computation of sums, averages, standard deviations, etc.&#x20;
* Collapsing of normalized tables into single tables to reduce joins.

The data mart output will produce a new database. This database's schema can be viewed in the datamart detail screen by selecting the **Schema** tab.

<figure><img src="../../../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure>

The schema tab shows an entity relationship diagram for the output schema. As illustrated above, the address, name and identifier tables have been de-normalized, and pivoted to allow for easy query writing.&#x20;
