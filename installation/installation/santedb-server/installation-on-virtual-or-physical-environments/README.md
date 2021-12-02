# Installation on Virtual or Physical Environments

You can install SanteDB iCDR on Microsoft Windows or Linux / Unix operations on x86 or ARM. The option to install SanteDB iCDR services on a full operating system is well suited for environments where:

* There is a need to finely tune the SanteDB configuration files
* There is a predefined TRA and PIA process which requires hardened / vetted operating system installations.
* There is existing Operating System environments in place, examples include:
  * Existing Application Performance Monitoring software which relies on a specific Operating System
  * Existing authentication/administration infrastructure (such as Active Directory)
  * Existing event log / notification shipping in infrastructure.
* There are requirements for hardware level isolation of the SanteDB services
* There are complex scaling requirements (such as using Windows scaling or clustered file servers)
* The environment's use of Windows only features in SanteDB. Windows only features include:
  * Using Microsoft Message Queue (MSMQ) dispatcher queues
  * Using Microsoft Windows Event Log notifications for central event monitoring
  * Using Microsoft Operation Manager to coordinate update and software package installation.

SanteDB supports  [installing-a-development-demo-environment.md](../installing-a-development-demo-environment.md "mention") and [installation-on-linux-and-unix.md](installation-on-linux-and-unix.md "mention").

## Pre-Requisites

If installing SanteDB iCDR on a native or virtualized operating system environments administrators will need to ensure the following pre-requisites are met:

* An appropriate operating system version is installed, patched and ready for installation of the SanteDB iCDR Application Server.
* An appropriate database environment (primarily PostgreSQL) is installed, patched and can accept connections from the SanteDB iCDR Application Server. &#x20;
