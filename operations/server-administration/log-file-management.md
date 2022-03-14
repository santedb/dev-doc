# Log File Management

## iCDR Log Files

iCDR log files are, by default, stored in the following directories:

* **Microsoft Windows Operating Systems:** `C:\Program Files\SanteSuite\SanteDB\Server`&#x20;
* **Linux Operating Systems:** `/opt/santesuite/santedb/server`
* **Docker:** `/var/log/`

Administrators can change the location of the log file changing the write location on the [diagnostics-configuration.md](host-configuration-file/diagnostics-configuration.md "mention")section and restarting the process.&#x20;

Log files are stored in a rolling name format `santedb_yyyyMMdd.log` and are never purged automatically.

{% hint style="info" %}
Administrators can setup scheduled tasks to remove or prune their log files according to their own operational policies.
{% endhint %}

## dCDR Log Files

dCDR log files are stored in the following locations:

* **Microsoft Windows Operating Systems:**&#x20;
  * dCDR Gateway: `%systemroot%\SysWOW64\config\systemprofile\local\log\`
  * dCDR Applications: `%localappdata%\log`
* **Linux Operating Systems:**
  * dCDR Gateway: `~root/.local/log`
  * dCDR Applications: `~/.local/log`
* **Docker**: `/root/.local/log`&#x20;

