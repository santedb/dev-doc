# Securing SanteDB Databases

When deploying SanteDB in production instances where personal health information (PHI) is stored, it is vital that the database contents be protected on disk. There are several manners in which this can be performed, each have considerations for performance, featureset, etc.

## Full-Disk Encryption

SanteDB iCDR and dCDR instances should use full disk encryption when deployed in production. This includes all application servers (web servers, app servers), database servers, and host machines.&#x20;

Full disk encryption protects your data when:

* The physical disk storing the files is stolen and taken to another computer.
* (When the VM enables this feature) The virtual hard disk file is copied/stolen from the host computer.

Full disk encryption does not protect your data if the disk is mounted on the host operating system. So, if an attacker gains access (such as SSH or RDP) to the server, this form of protection does not protect your data.

Full disk encryption solutions include: Microsoft Bitlocker, and LUKS on Linux. Devices running SanteDB on Android should also enable Android's device encryption feature.

## Transparent Data Encryption (TDE)

The next layer of encryption is TDE. TDE encrypts the files used by the database server (PostgreSQL, SQLite, etc.). TDE protects the data if the database files or (if using file based backup strategies) the backups are stolen.

TDE proects your data when:

* An attacker gains access to the database server via SSH or RDP and copies the database files.
* A backup file or media is stolen or lost.

TDE does not protect your data if an attacker can sign into the database server, or if your backups are performed using SQL dumps.

TDE is enabled by default on SanteDB when using SQLCipher and setting the `password` field on your connection string. Enabling TDE on PostgreSQL will require commercial support or the use of a special version of PostgreSQL (note: Version 16 of PostgreSQL, when available, has TDE listed as a feature in the open source version). TDE solutions for PostgreSQL include:

* [Fujitsu Enterprise PostgreSQL](https://www.postgresql.fastware.com/)
* [Enterprise DB PostgreSQL](https://www.enterprisedb.com/)
* [CyberTec PostgreSQL 12 TDE](https://www.cybertec-postgresql.com/en/transparent-data-encryption-installation-guide/)

## Application Level Encryption (ALE)

{% hint style="info" %}
This section describes a feature in SanteDB 3.0
{% endhint %}

SanteDB 3.0 introduces ALE. ALE is database intdependent and transparently handles the encryption of selected columns before they are written and/or read from the database. ALE can be used to selectively encrypt portions of the database. For example, when storing JOHN SMITH via any of the SanteDB APIs, the values are transparently encrypted so in the database an encrypted string is stored.

ALE has advantages in that:

* It protects your data even if the attacker can log into the database server.
* All SQL script-based backups are also encrypted.

ALE does, however, have some drawbacks, including:

* Columns that are encrypted using ALE can only be queried by exact match (i.e. SOUNDEX or LIKE no longer work on the data)
* Increased amount of data is stored in the database - as SanteDB will store information about the encrypted data in the column along with the encrypted value.
* Performance may suffer for reads and writes as data is encrypted and decrypted by the application server.
* Temporary constraints (currently being addressed):
  * Report which expose ALE fields are not transparently decrypted (this feature is currently being implemented)
  * Third party processes like ETL, BI, etc. aren't able to access the field data.
  * ALE initialization does not yet encrypt/decrypt existing data (this feature is currently being implemented on initialization)

ALE does not protect your data if a hacker gains access to the SanteDB APIs.&#x20;

### How ALE Works in SanteDB

In SanteDB ALE is comprised of the following components:

* **Application Master Key:** This is an X509 private/public key pair that is installed on application servers that are accessing data encrypted with ALE.
* **Symmetric Master Key:** This is a 256-bit random AES symmetric key that is stored in the database. This key is encrypted using the application master key's public key.
* **Encrypted Data:** Data in fields that are configured by the administrator is encrypted using an IV which is either randomly generated for each record, or deterministically generated based on the input data.&#x20;

The encryption is performed transparently to the applications using the data.&#x20;

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Enabling ALE

This feature is currently being documented.
