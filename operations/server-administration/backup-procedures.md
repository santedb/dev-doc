# Backup Procedures

The SanteDB iCDR and dCDR installed at clinics should be regularly backed up. As part of the [develop-operational-technology-architecture.md](../../installation/installation-1/planning-and-preparation-work/develop-operational-technology-architecture.md "mention") activities performed during the planning phase of your deployment, there should have been an effort to establish a Maximum Tolerable Outage (MTO).&#x20;

The MTO is the point at which it is tolerable to lose data. The obvious desire would be to never lose data, however the amount of additional equipment to provide that amount of system redundancy is almost always cost-prohibitive.&#x20;

This value of the MTO will dictate the frequency of your backup schedule. For example, if operating SanteMPI in a context where real-time registration is performed without any re-queueing mechanisms from the client, then that would mean data corruption of the SanteMPI server would result in lost data.&#x20;

If a backup is taken every 24 hours, then the maximum amount of data that would be lost in the case of a catastrophic failure would be the number of hours that have elapsed since the previous day's backup was completed.

## Backup of iCDR

The method of backup for the iCDR will depend on the requirements of your environment. The process of your backup and the system architecture of the backup design will depend somewhat on your recovery and storage space available. &#x20;

Whatever the method of backup, it is generally a good idea to keep backups of the iCDR in several places:

* **Online "Hot" Backups:** A "hot" backup should be online and accessible by the host environment and usually provides one or two of the most recent backups (imagine on a daily schedule that the previous 2 days of backups are kept). Example approaches include using:
  * Local Network Attached Storage (NAS) devices
  * Local Attached Disk devices
  * Cloud Based Storage options
* **Offline "Cold" Backups:** These are backups which are available only after media (such as tapes, removable media, etc.) is retrieved and restored. These are typically used for longer term backups and mitigate against active malware, randomware, or viruses which may lay dormant (i.e. a copy of the backup prior to infection can be restored). Examples include:
  * Tape / Removable Mass Media Storage
  * Disconnected disk devices

Additionally, copies of backups should be kept both in a location which is onsite (rapidly available for restoration) as well as offsite (in case of natural disaster, loss or damage to the data center).

| Backup Technology      | Benefits                                                                                                                                                                                                                                                               | Risks                                                                                                                                                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local NAS / SAN        | <ul><li>Fast network access to restore/backup data.</li><li>Complete control over the storage layout and redundancy.</li><li>Relatively inexpensive to operate ($/TB of storage)</li><li>COTS backup solutions support out of the box (via UNC, RSYNC, etc.)</li></ul> | <ul><li>Requires local administration to ensure operation.</li><li>May require separate offsite backup solution</li><li>NAS may be compromised by onsite issues (viruses, malware, ransomware, fires, etc.)</li></ul>              |
| Local Disk Devices     | <ul><li>Easy to setup (uses local disks and appears as mount-points)</li><li>Relatively cheap storage attached to server.</li><li>Fastest form of backup media.</li></ul>                                                                                              | <ul><li>Catastrophic loss of the server may result in loss of backups.</li><li>Compromised host (virus, malware, ransomware, fires, floods, etc.) would result in backups being unavailable.</li></ul>                             |
| Cloud Storage Provider | <ul><li>Easy to setup </li><li>Storage space is unlimited (depending on the plan)</li><li>Great offsite backup option </li></ul>                                                                                                                                       | <ul><li>Ongoing bandwidth, storage and cloud provider costs.</li><li>Uploading of larger backups is slower than via NAS.</li><li>Compromised cloud host provider or inappropriate setup may result in data breaches.</li></ul>     |
| Tape / Removable Media | <ul><li>Great for long-term storage of backups.</li><li>Can be shipped offsite and stored securely.</li><li>Large capacity of storage space is relatively cheap.</li></ul>                                                                                             | <ul><li>Can be easily lost/stolen and result in compromised data from backup.</li><li>Restoration can be time consuming</li><li>Requires physical access to the server infrastructure to remove/insert media for backup.</li></ul> |

### 3-2-1 Backup Strategy

The 3-2-1 backup strategy is highly recommended for use in production deployments of the SanteDB iCDR. This strategy is illustrated below.

* **3 Copies of Data:** At least 3 copies of the data should be available. At minimum the active (or primary copy) and at least 2 other copies should be available.
* **2 Different Media:** The copies of data should be stored on at least 2 different media or hosts. For example, the data exists on production server **and** a NAS **and** a cloud provider.
* **1 Copy Offsite:** At least one copy of the backup should always be kept offsite on a cloud provider or remote physical media.

There are many ways to realize this backup strategy using various technologies, to illustrate this, the SanteDB community server backup strategy is shown below:

&#x20;

![Basic 3-2-1 Backup Strategy](<../../.gitbook/assets/image (435).png>)

The backup on the community server:

1. Every night at 12:00 AM Microsoft Windows Server Backup performs an incremental backup of the most recent copy of all Virtual Disks from the physical host to a FreeNAS server using UNC Windows Shares and Volume Shadow Copy (live backups) to a fast pool (using SSD based disks in a RAID Z1). Snapshots of the fast pool are taken every 24 H and only 2 snapshots are kept on fast storage (2 days of backups). This pool is used for immediate restore if issues are detected within 24 H (**2 copies of the data now exist**)
2. The FreeNAS server then, every morning at 6:00 AM replicates the fast pool on SSD disks to a slow pool using 7200 RPM disks in RAID Z1. Snapshots of this pool are taken every 48 H and 30 snapshots are kept (30 days of backups). This pool is used for restore of infrastructure in the event data corruption occurred prior to a 48 H window (**3 copies of the data now exist**)
3. The FreeNAS server then, copies older snapshots from the slow storage pool to a physically attached USB hard drive. This hard drive has no limitation (beyond storage space) on snapshot lifetimes. After 30 days or earlier (when full), the drive is unmounted and stored at a different location.

The community server is not mission critical and therefore an MTO of months is permissible. If your deployment has a MTO value which indicates that only 24 H or 48 H of missing data is tolerable, then a different strategy should be employed.&#x20;

### Virtual Disk Backups

The simplest way to backup your SanteDB VM is to back up the virtual hard drives on which the SanteDB iCDR runs. This solution provides several advantages:

* Restoration of the iCDR is relatively straightforward (i.e. restore the VM)
* No need for special backup software or processes (many operating systems and hypervisors provide methods of copying VMs)
* &#x20;Incremental backups can be taken using snapshotting technology (for example, Hyper-V can perform live, in-flight backups using Volume Shadow Copies).
* No need to understand complex database restore procedures.

There are disadvantages to virtual disk backups, these can include:

* The amount of space required to store the files may be larger (this can be mitigated by separating "data" partitions from "OS" partitions and only backing up the data partitions)
* The amount of data which needs to be shared/shipped to network backups may be larger.
* Some hypervisors may require the VM to be shut down during backup

### Data Dump Backups

It is also possible to leverage database backups for your backup strategy of the iCDR. Implementers may use the built-in `pg_dump` backup method ([see tutorial here](https://snapshooter.com/learn/postgresql/pg\_dump\_pg\_restore)) or they may use a third party software tools ([see Bacula as an example](https://www.bacula.org/postgresql-backup-software/)).

The advantages of performing data dump backups are:

* Size of the backup files are typically smaller
* Does not rely on a hypervisor technology (works on bare-metal deployments, cloud deployments, docker, etc.)
* Data backups can be encrypted and compressed by piping output to different utilities

The disadvantages of performing data dump backups are:

* Restoration is more complex (requires a new PostgreSQL server to restore the copy of the data to, and often binary backups require the same version of PostgreSQL)
* Foreign key and data constraints can interrupt backup restore procedures.
* Slower to restore data (especially if using a SQL based dump).

To perform a backup of the SanteDB database you can use the following command:

```
pg_dump -h localhost -d DATABASE -E UTF8 -U username -W | gzip -e > backup.bak.gz
```

If you wish to encrypt and compress the backup, then you may additionally use the 7ZIP tool

```
pg_dump -h localhost -d DATABASE -E UTF8 -U username -W | 7z a -si -pSOMEPASSWORD backup.bak.7z -mhe=on
```

#### Restoring Data Dump Backups

Restoring a backup which was created using the data dump pattern is relatively straightforward process.

1. Decrypt your backup file (if you encrypted it)
2. Decompress the backup file
3. Run the contents through `pg_restore` or the `psql` command.

For example, to extract a backup to a new database called `newdb` from an encrypted backup in 7zip.

```bash
~$ psql -U postgres -h localhost -W 
-#: CREATE DATABASE newdb;
CREATE DATABASE
-#: \q
~$ 7z e mybackup.7z -so -pSOMEPASSWORD | psql -U postgres -h localhost --dbname=newdb -W
```

## Backup of dCDR&#x20;

The following dCDR products automatically backup their local database upon system service startup and according to the backup job in their software:

* SanteDB dCDR Gateway
* SanteDB dCDR Windows Client
* SanteDB dCDR Android Client

Each of these dCDR instances will provide a system job for the backup task

![](<../../.gitbook/assets/image (445).png>)

{% hint style="warning" %}
Backups are encrypted AES256 encryption with a passphrase matching the name of the device which produced the backup. It is important to keep the name of the machine in order to restore the backup.
{% endhint %}

Backup files can be accessed in the following locations:

* On Windows Operating Systems the backups are stored in `%appdata%\local\SanteDB\<instance-name>\backup`&#x20;
* On Linux Operating Systems backups are stored in `~/.local/SanteDB/<instance-name>/backup`
* On Android Operating Systems backups are stored in `~/Documents/SanteDB`

### Restoring dCDR Backups

To restore a dCDR backup is a straightforward process which differs based on the technology used.&#x20;

{% hint style="info" %}
Performing a restore will overwrite any data in the current dCDR instance. Ensure that all necessary data is properly synchronized prior to continuing a restore operation.
{% endhint %}

#### Restoring on dCDR Gateway

To restore on the dCDR gateway, administrators should run the `santedb-dcg` command with the `--restore` option:

```
C:\Program Files\SanteSuite\SanteDB\dCG\santedb-dcg --restore=<path_to_file> --sysrestore
```

{% hint style="info" %}
The `--sysrestore` should be used in an elevated command prompt on Windows and is used to restore the backup not to the current user's `%appdata%` directory but to the System `%appdata%` directory usually located in `C:\Windows\SysWOW64\config\systemprofile`.
{% endhint %}

You will be prompted for a backup password (the name of the original device which produced the backup). On Windows the restore process:

1. Shuts down the SanteDB dCDR (on Windows)
2. Decrypts and restores the data files to the appropriate directories
3. Starts the SanteDB dCDR (on Windows)

#### Restoring Windows Client

To restore files on the Windows (or Linux in the future) standalone clients, users should follow the process:

1. Ensure that the Windows application is configured with the same device name as the backup file.
2. Copy the `sdbk` file to the `%localappdata%\santedb\<instance-name>\restore` directory
3. Start the SanteDB Windows Application
4. Backup will automatically be processed and imported.

#### Restoring on Android

To restore a database on Android:

1. Ensure the `*.sdbk` file you want to restore is placed in the `Documents` folder of the tablet.
2. Wipe the data for the SanteDB dCDR application (in the Application Manager clear the data for the application)
3. Configure the application using the same tablet name and subscription settings as before
4. When prompted at startup, answer "YES" to the restore from backup prompt provided
