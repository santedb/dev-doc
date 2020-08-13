# Upgrading Gateway to SanteDB Langley \(v2.0.30+\) from SanteDB Kelowna and earlier

**Purpose:** You wish to upgrade a currently installed version of SanteDB Disconnected Gateway 2.0.2x to SanteDB Disconnected Gateway 2.0.3x.

**Introduction:** Starting with SanteDB Disconnected Gateway 2.0.3x , OpenSSL 1.1 is used as the encryption library rather than OpenSSL 1.02. This enhancement provides a more secure operating environment and also allows the Disconnected Gateway to use phonetic and levenshtein matches.

However, an in-place upgrade is no supported and an attempt to merely install and run a 2.0.3x instance over a 2.0.2x instance will result in a failed startup. This guide will walk administrators through the upgrade procedure.

**Applies To:**

* SanteDB Disconnected Gateway \(Langley - v2.0.30 and higher\) on Windows

**Steps:**

1. Navigate to your Disconnected Gateway administrative interface navigate to **System &gt; Jobs**
2. Locate the job **System Automatic Backup** and click the **Run** button
3. Allow the backup job to fully complete \(use the **Reload** button to refresh the current status\).
4. Navigate to C:\Windows\SYSWOW64\config\systemprofile\AppData\Local\SanteDB\dcg-default\backups
5. Locate the most recent backup file and copy it \(press CTRL+C\)
6. Navigate to C:\Windows\SYSWOW64\config\systemprofile\AppData\Local\SanteDB\dcg-default 
7. Create a directory called **Restore** and paste \(CTRL+V\) the copied backup file.
8. Install SanteDB Disconnected Gateway 2.0.30+ as normal

