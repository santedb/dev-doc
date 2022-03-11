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

### Backup Pipeline

The best solution for a backup technology for SanteMPI iCDR products is often a combination of the onsite/offsite backups with varying technology. For example, the SanteDB community servers use a staged approach as illustrated in .

&#x20;

![](<../../.gitbook/assets/image (435).png>)

The backup on the community server:

1. Every night at 12:00 AM Microsoft Windows Server Backup performs an incremental backup of the most recent copy of all Virtual Disks from the physical host to a FreeNAS server using UNC Windows Shares and Volume Shadow Copy (live backups) to a fast pool (using SSD based disks in a RAID Z1). Snapshots of the fast pool are taken every 24 H and only 2 snapshots are kept on fast storage (2 days of backups). This pool is used for immediate restore if issues are detected within 24 H
2. The FreeNAS server then, every morning at 6:00 AM replicates the fast pool on SSD disks to a slow pool using 7200 RPM disks in RAID Z1. Snapshots of this pool are taken every 48 H and 30 snapshots are kept (30 days of backups). This pool is used for restore of infrastructure in the event data corruption occurred prior to a 48 H window.
3. The FreeNAS server then, every month, copies any old snapshots from the slow storage pool to a physically attached USB hard drive. This hard drive has no limitation (beyond storage space) on snapshot lifetimes.&#x20;

### Virtual Disk Backups

The simplest way to backup your SanteDB VM is to back up the virtual hard drives on which the SanteDB iCDR runs. This solution provides several advantages:

* Restoration of the iCDR is relatively straightforward (i.e. restore the VM)
* No need for special backup software or processes (many operating systems and hypervisors provide methods of copying VMs)
* &#x20;Incremental backups can be taken using snapshotting technology (for example, Hyper-V can perform live, in-flight backups using Volume Shadow Copies).

There are disadvantages to virtual disk backups, these can include:

* The amount of space required to store the files may be larger (this can be mitigated by separating "data" partitions from "OS" partitions and only backing up the data partitions)
* The amount of data which needs to be shared/shipped to network backups may be larger.
* Some hypervisors may require the VM to be shut down during backup

####
