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

SanteDB 3.0 introduces ALE. ALE is database intdependent and transparently handles the encryption of selected columns before they are written and/or read from the database. ALE can be used to selectively encrypt portions of the database.&#x20;

For example, by default the SanteDB entity name table may appear as:

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

However, when ALE is enabled, the data in the database column appears as:

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The original values remain for any of the SanteDB APIs, the values are transparently encrypted so in the database an encrypted string is stored.

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

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

### Enabling ALE

When ALE is enabled in the Configuration Tool via the `Application Level Encryption` option , the configuration tool will either encrypt or decrypt the entire database. When enabled via configuration, existing data is encrypted or decrypted on service start.&#x20;

To enable, ALE, in a supported `<section>` element in your configuration file, add the `<aleConfiguration>` element.&#x20;

```xml
<aleConfiguration enabled="true">
  <certificate findType="FindByThumbprint" 
      storeName="My" 
      storeLocation="CurrentUser" 
      findValue="e3829c6d1db995abcc4fc0a1a7cde9445e411e10"/>
  <saltSeed>AEAD43FD3E4FE3FDB432F032348090232F</saltSeed>
  <!-- Need exact matching -->
  <field mode="deterministic">entity.identifier</field>
  <!-- Need exact matching -->
  <field mode="deterministic">address.component</field>
  <!-- Need soundex and levenshtein so no encryption -->
  <field mode="off">name.component</field>
  <!-- Don't need to query by note text -->
  <field mode="random">entityNote.text</field>

</aleConfiguration>
```

The configuration attributes are:

* **enabled**: Enables the global ALE system.
* **field:** The fields to be enabled for encryption, wth the specified mode:
  * **deterministic:** Each field is encrypted with an IV based on the input value. When deterministic mode is enabled, the data is encrypted in a way that queries may still be executed on the fields, however multiple fields with the same un-encrypted value will have the same ciphertext, and thus, this method is less secure.
  * **random**: Each field is encrypted with a unique IV generated randomly. When this mode is enabled, any ALE fields **CANNOT BE QUERIED** , rather the data is securely stored in the database file.
  * **off**: Disables the ALE encryption. If a database was previously encrypted, the data in the columns will be decrypted.
* **certificate:** This specifies the application master key in your application server's secure certificate store (note: you can also use the `--reencrypt` prompt to select the certificate)
* **saltSeed:** To better protect the values encrypted using **deterministic** mode (to prevent rainbow value attacks) the IV and encrypted values are salted using this value as a seed. This value should be a 128-bit number.

After configuring ALE, stop the SanteDB host process on all application servers:&#x20;

{% tabs %}
{% tab title="Windows" %}
```
net stop santedb
santedb --config=santedb.config.xml --reencrypt
net start santedb
```
{% endtab %}

{% tab title="Linux" %}
```
sudo systemctl stop santedb
sudo mono /opt/santedb/santedb.exe --config=/opt/santedb/santedb.config.xml --reencrypt
sudo systemctl start santedb
```


{% endtab %}
{% endtabs %}

{% hint style="info" %}
When ALE is enabled via the --reencrypt option, your configuration file will be protected.
{% endhint %}

#### Configuration Tool

You can enable and change the ALE parameters using the Configuration Tool under `Security -> Application Layer Encryption.`

<figure><img src="../../../.gitbook/assets/image (529).png" alt=""><figcaption></figcaption></figure>

### Disabling/Changing ALE Parameters

If, for any reason, the ALE parameters need to be disabled or changed, you must instruct SanteDB to decrypt the database fields (prior optionally to re-encrypting them with another key).&#x20;

The first step is to allow SanteDB to decrypt the database, this is done by changing `aleMode="deterministic"` to `aleMode="off"` and allowing SanteDB to process the ALE change with the `--test-start` option.

When this operation is complete, the ALE parameters (such as fields, or keys) can be changed, and the database is then re-encrypted with the new settings.

{% hint style="danger" %}
It is important, in the decryption process that the existing ALE settings for key and fields do not change - as these may impede the decryption and re-encryption process.
{% endhint %}

### Key Rotation

There may arise a time when you need to change the application master key or symmetric master key due to certificate expiration, disclosure, etc. To perform key rotation, SanteDB needs to decrypt your ALE data, and then re-encrypt it using the new parameters. This process can be performed by running:

```
santedb --reencrypt --config=santedb.config.xml
```

{% hint style="danger" %}
To not modify your `santedb.config.xml` file prior to running this command. Your configuration file should contain the settings for the current ALE settings. The key rotation will automatically set your configuration file with the new certificate parameters.
{% endhint %}

{% hint style="warning" %}
You will need to propogate your configuration to other SanteDB server hosts if you are running with multiple application servers.
{% endhint %}

{% hint style="info" %}
You can disable ALE by entering an empty value when prompted for the new ALE encryption certificate thumbprint.
{% endhint %}
