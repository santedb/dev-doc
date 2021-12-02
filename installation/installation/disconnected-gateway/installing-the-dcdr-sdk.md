# Installing the dCDR SDK

In order to start writing your own applets you're going to need the following environment setup:

* An HTML & JavaScript editor (Microsoft Visual Studio Code works well)
* Windows Environments:
  * [Microsoft Visual C++ 2015 - 2019 Runtime](https://download.visualstudio.microsoft.com/download/pr/3b070396-b7fb-4eee-aa8b-102a23c3e4f4/40EA2955391C9EAE3E35619C4C24B5AAF3D17AEAA6D09424EE9672AA9372AEED/VC\_redist.x64.exe)
  * .NET Framework 4.7.2 or higher
* Linux / Mac Environments:
  * Mono Framework (if running on MacOS or Linux)&#x20;
* The SanteDB SDK ([https://github.com/santedb/santedb-sdk/releases](https://github.com/santedb/santedb-sdk/releases))&#x20;
* Chrome or Edge are recommended for debugging
* Optional: Setup a iCDR Server Instance

## Installing the SDK

### Windows

Installation on Windows Environments requires running the packaged Windows installer which will install the necessary files into `C:\Program Files\SanteSuite\SDK`. You can launch a command prompt with this location on your path using the start menu shortcut.

### Linux

In Linux the installation procedure for the SDK requires installing mono. This can be done by following the [Installation Instructions](https://www.mono-project.com/download/stable/#download-lin) for your distribution, on Ubuntu you can install Mono using:

`sudo apt install mono-complete`

The software requires at least mono version 5.x , so after installation you can run `mono --version` to obtain the version code:

```
$ mono --version
Mono JIT compiler version 6.12.0.90 (tarball Fri Sep  4 14:01:23 UTC 2020)
Copyright (C) 2002-2014 Novell, Inc, Xamarin Inc and Contributors. www.mono-project.com
    TLS:           __thread
    SIGSEGV:       altstack
    Notifications: epoll
    Architecture:  amd64
    Disabled:      none
    Misc:          softdebug 
    Interpreter:   yes
    LLVM:          yes(610)
    Suspend:       hybrid
    GC:            sgen (concurrent by default)
```

After the mono project is installed, you can extract the provided tarball to a directory of convenience (like /opt/santedb-sdk or /usr/local/santedb-sdk). All commands in this tutorial on Linux should be prefixed with mono, so for example:

`mono /opt/santedb-sdk/sdb-ade.exe --help`

## Configuring the SDK

Next, you'll need to configure the SDK to use a server endpoint. This endpoint is the iCDR to which your dCDR will connect. There are a variety of ways you can connect to the iCDR (such as offline mode, etc.) however we'll connect the SDK using online mode only. This means that your SDK environment will need to be connected to the internet and have contact with the remote server to function.

We'll use the elbonia.santesuite.net server for our debugging. First we should launch the sdb-ade command which is the debugging tool for the dCDR:

```
sdb-ade --ref=santedb.admin.sln.pak
```

{% hint style="info" %}
If you want to debug the core applets you can clone the [https://github.com/santedb/applets](https://github.com/santedb/applets) directory and reference the solution file santedb.admin.sln.xml with --ref=\<path-to-applets>/santedb.admin.sln.xml
{% endhint %}

If successful you should see the initial configuration window.

![](<../../../.gitbook/assets/image (196).png>)

If you have a local iCDR server you would enter the details for this server now, for the Elbonia MPI the settings are:

* address => elbonia.santesuite.net
* Port => 8443
* Use TLS => True

Upon clicking the join button you'll be prompted to enter the credentials of the user which is joining your dCDR device to the domain:

![](<../../../.gitbook/assets/image (197).png>)

For the demonstration server you can use demoadmin/@Elbonia123 .

If successful, you should receive a welcome message to the domain. You will then need to select a role, normally, when deploying the dCDR, this setting indicates the user interface and plugins that the client should download. For the SDK these settings are ignored.

![](<../../../.gitbook/assets/image (194).png>)

After selecting the role, you must configure the synchronization settings. Using "Online Only" will allow you to get an SDK environment setup quickly that mimics the web portal installation.

{% hint style="info" %}
There are currently known issues with the Synchronized mode setup with some community plugins (namely the reading of custom synchronization subscriptions). It is recommended, for now, using Online Only option for development.
{% endhint %}

![](<../../../.gitbook/assets/image (190).png>)

You can continue setup by accepting the defaults for the other pages. Some configuration notes:

* Turn down logging to Errors and Warnings if you value your sanity (and you want performance similar to production)
* You can turn off optimization if you receive errors about GZIP CRC checksums (there is a known issue certain server middleware)
* If you're using a proxy (like fiddler) for debugging you should enter the full proxy address and port (for fiddler use [http://localhost:8888](http://localhost:8888))

Upon completion you will be instructed to restart the application host. This is done by pressing CTRL+C in the sdb-ade window and restarting it.

![](<../../../.gitbook/assets/image (189).png>)

