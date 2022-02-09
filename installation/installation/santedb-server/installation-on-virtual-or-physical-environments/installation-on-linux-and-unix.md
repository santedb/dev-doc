# Installation on Linux and Unix

{% hint style="info" %}
This section is currently being written. Check back soon for instructions on installing on Linux physical and virtual environments.&#x20;
{% endhint %}



When installing SanteDB iCDR server on Linux or Unix based environment you should use the tarballs for the latest version of the SanteDB iCDR server. Each solution within SanteDB iCDR Server has its own distribution which can be downloaded for their own source repository.&#x20;

* [SanteDB iCDR Releases](https://github.com/santedb/santedb-server/releases)
* [SanteMPI Releases](https://github.com/santedb/santempi/releases)

The installation process for SanteDB on Linux is the same process as installation on Windows::

1. Install the software
   * Copy software program files and pre-requisites&#x20;
   * Initiate the configuration process
2. Configuration of the software
   * Customizing the behavior of the installed plugins
   * Entering implementation specific details about the deployment
3. Running/Initializing the Server

The tarballs provided have been written for and test on Debian based distributions, manual installation for non-Debian based distributions is required.

## System Requirements



When running SanteDB iCDR server on Unix based operating systems you will require, at minimum:

* One of the following Unix operating systems:
  * MacOS X 10.9 on M1 or x86 (manual installation)
  * Ubuntu 16.04 or later (install script)
  * Debian 9 or later (install script)
  * CentOS or RHEL 6 or better (manual installation)
* 2 Core CPU (4 to 8 Cores recommended)
* 2 GB RAM (8 or 16 GB of RAM recommended)
* 300 MB of disk space (1 GB recommended)

Users should be familiar with basic Unix concepts such as:

* Un-taring archive files
* Basic familiarity with Unix commands

## Installation

### Using the Install Script

{% hint style="info" %}
The installation script has been tested on Ubuntu 18.04 and 20.04 and Debian 10
{% endhint %}

To install the SanteDB iCDR 2.1.140 or higher via the installation script provided, you should first extract the tarball contents:

```
$ tar -xjvf santedb-server-2.1.140.tar.bz2
```

This will extract the software to the `./santedb-server-2.1.140` directory. You can enter that directory and run the `install.sh` script:

```
$ cd santedb-server-2.1.140/
santedb-server-2.1.140 $ chmod +x install.sh
santedb-server-2.1.140 $ ./install.sh 
```

If you are not running the script as root, the installer will prompt if you would like it to use SUDO. The script will then detect pre-requisites for mono and postgresql. The install script will install mono for you.

{% hint style="info" %}
If you're installing SanteDB iCDR with postgresql running on a different host, you can decline the installation of PostgreSQL. Installation of `mono` is required.
{% endhint %}

{% hint style="info" %}
If you receive an error `cannot find package mono-complete` you may need to run an `apt update` on your system to include the mono packages on Ubuntu. If running Ubuntu 18.04 or prior or Debian 9 you can follow the [Mono Framework Installation](https://www.mono-project.com/download/stable/#download-lin-ubuntu) guide.
{% endhint %}

Finally, you'll be prompted for an installation target, the default location is `/opt/santesuite/santedb/server/`, you can accept the default or change the location of installation to suit your policy.

After installation is complete, the default SanteDB publisher certificates will be registered with the Mono trust store and you'll be provided the option to setup SanteDB as a daemon.&#x20;

### Manual Installation

When installing the SanteDB iCDR server manually, administrators should ensure that the pre-requisites for SanteDB are installed on their preferred Unix environment:

* [Mono Framework 5](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
* [PostgreSQL 10](https://www.postgresql.org/?&)

Once installed, users should create their target installation directory (this tutorial will use `/opt/santedb` , and should unzip the tarball or zip file to that location.

```
tar xjvf santedb-server-2.1.140.tar.bz2
mkdir -p /opt/santedb
mv santedb-server-2.1.140 /opt/santedb
cd /opt/santedb
```

You then need to install the SanteDB publisher certificates into the Mono certificate store:

```
sudo mono SanteDB.exe --install-certs
```

Finally, you can run the configuration tool in your installation directory with

```
sudo mono ConfigTool.exe
```

#### Setting SanteDB as a Daemon

You can register SanteDB as a daemon on your distribution of Linux by creating a service definition file. This is done by creating a new file at `/etc/systemd/system/santedb.service` and using the contents:

```ini
[Unit]
Description=SanteDB iCDR Server

[Service]
Type=simple
RemainAfterExit=yes
ExecStart=/usr/bin/mono-service -d:$INSTALL_ROOT /opt/santesuite/santedb/server/SanteDB.exe --console 
ExecStop=kill \`cat /tmp/SanteDB.exe.lock\`

[Install]
WantedBy=multi-user.target
```

After this time you can run `systemctl reload-daemons` to load your service definition.

## Configuring SanteDB iCDR

SanteDB's configuration tool on linux uses the Mono to GTK+ WinForms implementation. The application is the same application as documented in the [configuration-tool](../../../../operations/server-administration/configuration-tool/ "mention") documentation.

![](<../../../../.gitbook/assets/image (437) (1) (1) (1) (1) (1) (1).png>)

Details on the initial configuration of SanteDB can be followed from the [Windows Installation](../installing-a-development-demo-environment.md) guide.

{% hint style="info" %}
While the configuration tool runs on Linux it is not regularly tested and has known rendering and incompatibilities. Linux users can use the configuration tool to generate basic configurations, however advanced operations (like certificate binding, service control, etc.) may not function as expected. Linux users are encouraged to use the [host-configuration-file](../../../../operations/server-administration/host-configuration-file/ "mention")
{% endhint %}

## Initial Run / Initialization

Like the Windows installation, the SanteDB, the SanteDB iCDR on Linux needs to be initialized, unlike windows this requires manual stop/start of the service.

If you've installed SanteDB as a daemon the command to stop or start the daemon is:

```
systemctl stop santedb
```

If you are running SanteDB on a console, you can run:

```
mono /opt/santesuite/santedb/server/SanteDB.exe --console
```

### Validating Installation

Once started you can validate connectivity to the SanteDB iCDR server running the SanteDB Administration Console. The Administration console is executed using:

```
mono /opt/santesuite/santedb/server/sdbac.exe
```

Once the login prompt is available you can login with `Administrator` and password `Mohawk123`.

```
SanteDB Administration & Security Console v2.1.131.0 (Queenston)
Copyright (C) 2015 - 2020, SanteSuite Community Partners (see NOTICES)
Access denied, authentication required.
Username:administrator
Password:************
* http://localhost:8080/ami -> v.2.1.116.0 (Queenston)
Ready...
>
```

### Service Management

If the option to install the SanteDB iCDR as a Linux daemon was selected during install, then the service can be controlled with `systemctl` for example:

```
sudo systemctl start santedb
sudo systemctl status santedb
```

Stopping the service is done with the same command:

```
sudo systemctl stop santedb
sudo systemctl status santedb
```

The service can be enabled on startup using:

```
sudo systemctl enable santedb
```

{% hint style="info" %}
The `/tmp/SanteDB.exe.lock` file contains the PID of the running SanteDB instance. Kill commands such as `SIGHUP` , `SIGKILL` and `SIGSEV` can be sent to this PID to terminate the SanteDB daemon.
{% endhint %}
