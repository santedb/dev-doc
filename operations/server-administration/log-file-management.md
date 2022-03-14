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

## Log Format

Log files for the dCDR and iCDR have a format as described below:

```
Source@ThreadID <Level> [TIMESTAMP]: Log Message
```

For example, this log entry indicates an ERROR on 2021-01-05 from the FHIR plugin on thread 7:

```
SanteDB.Messaging.FHIR@RSRVR-ThreadPoolThread-7 <Error> [2021-01-05T00:45:15.9914111-05:00]: Error on WCF FHIR Pipeline: SanteDB.Core.Exceptions.PolicyViolationException: Policy '1.3.6.1.4.1.33349.3.1.5.9.2.2.0' was violated by 'Administrator' with outcome 'Deny'
```

Using the ThreadID is helpful when diagnosing issues in a production environment as it allows for the tracking of a client's execution pathway through the solution.
