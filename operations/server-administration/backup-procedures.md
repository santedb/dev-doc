# Backup Procedures

The SanteDB iCDR and dCDR installed at clinics should be regularly backed up. As part of the [develop-operational-technology-architecture.md](../../installation/installation-1/planning-and-preparation-work/develop-operational-technology-architecture.md "mention") activities performed during the planning phase of your deployment, there should have been an effort to establish a maximum tolerable outage (MTO).&#x20;

The MTO is the point at which it is tolerable to lose data. This value will dictate the frequency of your backup schedule. For example, if operating SanteMPI in a context where real-time registration is performed without any re-queueing mechanisms from the client, then that would mean data corruption of the SanteMPI server would result in lost data.&#x20;

If a backup is taken every 24 hours, then the maximum amount of data that would be lost in the case of a catastrophic failure would be the number of hours to restore backup since the previous day's backup.

## Backup of iCDR

The method of backup for the iCDR will depend on the requirements of your environment. The process of your backup and the architecture of the backup will depend on your recovery and storage space available. &#x20;

Whatever the method of backup, it is generally a good idea to keep backups of the iCDR in several places:

* **Online Backups:** A hot backup should be available to the host environment and usually keeps one or two of the most recent backups (imagine on a daily schedule that the previous 2 days of backups are kept). Examples include:
  * Local Network Attached Storage (NAS) devices
  * Local Attached Disk devices
  * Cloud Based Storage options
* **Cold / Offline Backups:** These are backups which are available only after media (such as tapes, removable media, etc.) is retrieved and restored. These are typically used for longer term backups and mitigate against malware, randomware, or viruses which may lay dormant (i.e. a copy of the backup prior to infection can be restored). Examples include:
  * Tape / Removable Mass Media Storage

Additionally, backups should be kept in a location which is onsite (rapidly available for restoration) as well as copies kept offsite (in case of natural disaster or loss of the data center).

| Backup Technology      | Benefits                                                                                                                                                                                                                                                               | Risks                                                                                                                                                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local NAS / SAN        | <ul><li>Fast network access to restore/backup data.</li><li>Complete control over the storage layout and redundancy.</li><li>Relatively inexpensive to operate ($/TB of storage)</li><li>COTS backup solutions support out of the box (via UNC, RSYNC, etc.)</li></ul> | <ul><li>Requires local administration to ensure operation.</li><li>May require separate offsite backup solution</li><li>NAS may be compromised by onsite issues (viruses, malware, ransomware, fires, etc.)</li></ul>              |
| Local Disk Devices     | <ul><li>Easy to setup (uses local disks and appears as mount-points)</li><li>Relatively cheap storage attached to server.</li><li>Fastest form of backup media.</li></ul>                                                                                              | <ul><li>Catastrophic loss of the server may result in loss of backups.</li><li>Compromised host (virus, malware, ransomware, fires, floods, etc.) would result in backups being unavailable.</li></ul>                             |
| Cloud Storage Provider | <ul><li>Easy to setup </li><li>Storage space is unlimited (depending on the plan)</li><li>Great offsite backup option </li></ul>                                                                                                                                       | <ul><li>Ongoing bandwidth, storage and cloud provider costs.</li><li>Uploading of larger backups is slower than via NAS.</li><li>Compromised cloud host provider or inappropriate setup may result in data breaches.</li></ul>     |
| Tape / Removable Media | <ul><li>Great for long-term storage of backups.</li><li>Can be shipped offsite and stored securely.</li><li>Large capacity of storage space is relatively cheap.</li></ul>                                                                                             | <ul><li>Can be easily lost/stolen and result in compromised data from backup.</li><li>Restoration can be time consuming</li><li>Requires physical access to the server infrastructure to remove/insert media for backup.</li></ul> |

### 3-2-1 Backup Strategy

The 3-2-1 backup strategy is highly recommended for use in production deployments of the SanteDB iCDR. This strategy is illustrated below.

* **3 Copies of Data:** At least 3 copies of the data should be available. At minimum the active or primary copy and at least 2 other copies.
* **2 Different Media:** The copies of data should be stored on at least 2 different media or hosts. For example, the data exists on production server **and** a NAS **and** a cloud provider.
* **1 Copy Offsite:** At least one copy of the backup should always be kept offsite on a cloud provider or physical media.

There are many ways to realize this backup strategy using various technologies, to illustrate this, the SanteDB community server backup strategy is shown below:

&#x20;

![](<../../.gitbook/assets/image (432).png>)

The backup on the community server:

1. Every night at 12:00 AM Microsoft Windows Server Backup performs an incremental backup of the most recent copy of all Virtual Disks from the physical host to a FreeNAS server using UNC Windows Shares and Volume Shadow Copy (live backups) to a fast pool (using SSD based disks in a RAID Z1). Snapshots of the fast pool are taken every 24 H and only 2 snapshots are kept on fast storage (2 days of backups). This pool is used for immediate restore if issues are detected within 24 H (**2 copies of the data now exist**)
2. The FreeNAS server then, every morning at 6:00 AM replicates the fast pool on SSD disks to a slow pool using 7200 RPM disks in RAID Z1. Snapshots of this pool are taken every 48 H and 30 snapshots are kept (30 days of backups). This pool is used for restore of infrastructure in the event data corruption occurred prior to a 48 H window (**3 copies of the data now exist**)
3. The FreeNAS server then, copies older snapshots from the slow storage pool to a physically attached USB hard drive. This hard drive has no limitation (beyond storage space) on snapshot lifetimes. When full, the drive is unmounted and stored at a different location.

The community server is not mission critical and therefore an MTO of months is permissible. If your deployment has a MTO value which indicates that only 24 H or 48 H of missing data is tolerable, then a different strategy may be employed.&#x20;

### Virtual Disk Backups

The simplest way to backup your SanteDB VM is to back up the virtual hard drives on which the SanteDB iCDR runs. This solution provides several advantages:

* Restoration of the iCDR is relatively straightforward (i.e. restore the VM)
* No need for special backup software or processes (many operating systems and hypervisors provide methods of copying VMs)
* &#x20;Incremental backups can be taken using snapshotting technology (for example, Hyper-V can perform live, in-flight backups using Volume Shadow Copies).
* No need to fiddle with database restore procedures.

There are disadvantages to virtual disk backups, these can include:

* The amount of space required to store the files may be larger (this can be mitigated by separating "data" partitions from "OS" partitions and only backing up the data partitions)
* The amount of data which needs to be shared/shipped to network backups may be larger.
* Some hypervisors may require the VM to be shut down during backup

### Data Dump Backups

It is also possible to leverage database backups for your backup strategy of the iCDR. Implementers may use the build-in `pg_dump` backup method ([see tutorial here](https://snapshooter.com/learn/postgresql/pg\_dump\_pg\_restore)) or they may use a third party software tools ([see Bacula as an example](https://www.bacula.org/postgresql-backup-software/)).

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
