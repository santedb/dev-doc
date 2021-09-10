# Getting Started

In order to start writing your own applets you're going to need the following environment setup:

* An HTML & JavaScript editor \(Microsoft Visual Studio Code works well\)
* Windows Environments:
  * [Microsoft Visual C++ 2015 - 2019 Runtime](https://download.visualstudio.microsoft.com/download/pr/3b070396-b7fb-4eee-aa8b-102a23c3e4f4/40EA2955391C9EAE3E35619C4C24B5AAF3D17AEAA6D09424EE9672AA9372AEED/VC_redist.x64.exe)
  * .NET Framework 4.7.2 or higher
* Linux / Mac Environments:
  * Mono Framework \(if running on MacOS or Linux\) 
* The SanteDB SDK \([https://github.com/santedb/santedb-sdk/releases](https://github.com/santedb/santedb-sdk/releases)\) 
* Chrome or Edge are recommended for debugging
* Optional: Setup a iCDR Server Instance

## Installing the SDK

### Windows

Installation on Windows Environments requires running the packaged Windows installer which will install the necessary files into `C:\Program Files\SanteSuite\SDK`. You can launch a command prompt with this location on your path using the start menu shortcut.

### Linux

In Linux the installation procedure for the SDK requires installing mono. This can be done by following the [Installation Instructions](https://www.mono-project.com/download/stable/#download-lin) for your distribution, on Ubuntu you can install Mono using:

`sudo apt install mono-complete`

The software requires at least mono version 5.x , so after installation you can run `mono --version` to obtain the version code:

```text
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

After the mono project is installed, you can extract the provided tarball to a directory of convenience \(like /opt/santedb-sdk or /usr/local/santedb-sdk\). All commands in this tutorial on Linux should be prefixed with mono, so for example:

`mono /opt/santedb-sdk/sdb-ade.exe --help`

## Obtain the Starter Code

Next, you'll need to clone or create an applet. You can clone the starter applet from [https://github.com/santedb/applet-starter](https://github.com/santedb/applet-starter) in any directory of your choice.

![](../../../../.gitbook/assets/image%20%28193%29.png)

## Configuring the SDK

Next, you'll need to configure the SDK to use a server endpoint. This endpoint is the iCDR to which your dCDR will connect. There are a variety of ways you can connect to the iCDR \(such as offline mode, etc.\) however we'll connect the SDK using online mode only. This means that your SDK environment will need to be connected to the internet and have contact with the remote server to function.

We'll use the elbonia.santesuite.net server for our debugging. First we should launch the sdb-ade command which is the debugging tool for the dCDR:

```text
sdb-ade --ref=santedb.admin.sln.pak --applet=path-to-applet-starter
```

This command instructs the applet debugging environment to:

1. Include / reference the contents of the administrative portal \(--ref\)
2. Debug the applet-starter directory

{% hint style="info" %}
If you want to debug the core applets you can clone the [https://github.com/santedb/applets](https://github.com/santedb/applets) directory and reference the solution file santedb.admin.sln.xml with --ref=&lt;path-to-applets&gt;/santedb.admin.sln.xml
{% endhint %}

If successful you should see the initial configuration window.

![](../../../../.gitbook/assets/image%20%28196%29.png)

If you have a local iCDR server you would enter the details for this server now, for the Elbonia MPI the settings are:

* address =&gt; elbonia.santesuite.net
* Port =&gt; 8443
* Use TLS =&gt; True

Upon clicking the join button you'll be prompted to enter the credentials of the user which is joining your dCDR device to the domain:

![](../../../../.gitbook/assets/image%20%28197%29.png)

For the demonstration server you can use demoadmin/@Elbonia123 .

If successful, you should receive a welcome message to the domain. You will then need to select a role, normally, when deploying the dCDR, this setting indicates the user interface and plugins that the client should download. For the SDK these settings are ignored.

![](../../../../.gitbook/assets/image%20%28194%29.png)

After selecting the role, you must configure the synchronization settings. Using "Online Only" will allow you to get an SDK environment setup quickly that mimics the web portal installation.

{% hint style="info" %}
There are currently known issues with the Synchronized mode setup with some community plugins \(namely the reading of custom synchronization subscriptions\). It is recommended, for now, using Online Only option for development.
{% endhint %}

![](../../../../.gitbook/assets/image%20%28190%29.png)

You can continue setup by accepting the defaults for the other pages. Some configuration notes:

* Turn down logging to Errors and Warnings if you value your sanity \(and you want performance similar to production\)
* You can turn off optimization if you receive errors about GZIP CRC checksums \(there is a known issue certain server middleware\)
* If you're using a proxy \(like fiddler\) for debugging you should enter the full proxy address and port \(for fiddler use [http://localhost:8888\](http://localhost:8888\)\)

Upon completion you will be instructed to restart the application host. This is done by pressing CTRL+C in the sdb-ade window and restarting it.

![](../../../../.gitbook/assets/image%20%28189%29.png)

## Hello World!

If you re-run the command `sdb-ade --ref=santedb.admin.sln.pak --applet=path-to-applet-starter` you'll notice that upon login you see the administrative panel. This is because the --ref= is instructing the SDK that your module is extending the admin panel.

To debug just the applet-starter applet you can instead reference just the core plugins:

```text
sdb-ade --ref=santedb.core.sln.pak --applet=path-to-applet-starter
```

The browser will launch with the basic login.html contents, which you can login with demoadmin/@Elbonia123.

{% hint style="info" %}
The login screen is shown because the index.html view demands login permission to be rendered. By default the dCDR interface will display the default AngularJS route of /
{% endhint %}

After logging in, you should see the welcome message:

![](../../../../.gitbook/assets/image%20%28192%29.png)

### Code Editing

You can now edit the files in your favorite HTML/JavaScript editor. After editing a file you simply need to press the refresh button on the browser window. We can also update the code to query some patients from the database, if we modify the contents of index.html:

```markup
<div>
    <form name="searchForm" ng-submit="doSearch(searchForm)" method="dialog">
        Search For: <input 
            required="required" minlength="3" maxlength="30" 
            type="text" ng-model="searchTerm" />
        <button type="submit">{{ 'ui.action.search' | i18n }}</button>
    </form>
    <table border="1">
        <tr ng-repeat="result in results.resource">
            <td>{{ result.name | name }}</td>
        </tr>
    </table>
</div>
```

This code:

* Creates a new form which calls the doSearch function in the controller
* Allows the user to enter a text search term
* Renders the results in the bundle

{% hint style="info" %}
All HTML in SanteDB must be well-formed XHTML placed in the [http://www.w3.org/1999/xhtml](http://www.w3.org/1999/xhtml) namespace.
{% endhint %}

We can then edit the index.js controller file to actually perform our search:

```javascript
$scope.doSearch = doSearch;

// Perform a search 
async function doSearch(searchForm) {
    if(searchForm.$invalid) {
        alert("Invalid Input!");
        return;
    }

    try {
        $scope.results = await SanteDB.resources.patient.findAsync({ "name.component.value" : `~${$scope.searchTerm}` });
    } catch (e) {
        $rootScope.errorHandler(e);
    }
}
```

This code:

* Validates that the form has no issues
* Calls the SanteDB API to find all patients \(SanteDB.resources.patient.findAsync\) who has any name \(name.component.value\) is approximately the output \(the ~ indicator\)
* Assigns the results of the call to the scoped results variable

![](../../../../.gitbook/assets/image%20%28191%29.png)

### Next Steps

For an example of a more complex applet which extends the underlying administrative panel, you can clone the elb-mpi project and launch the debugger with that codebase:

```javascript
sdb-ade --ref=santedb.admin.sln.pak --applet=path-to-elb-mpi
```

When launching this you should be presented with the Elbonia customizations of the MPI administrative panel.

![](../../../../.gitbook/assets/image%20%28195%29.png)

### Useful Hints

* You can reset your debugging environment with the `sdb-ade --reset` option
* You can setup different servers/environments by adding the --name= option, for example, you can setup a PROD and STAGE debugging environment by using `sdb-ade --ref=XXX --name=PROD` and `sdb-ade --ref=YYY --name=STAGE`
* You can change the configuration of your debugging environment and/or see offline files in the following directory:
  * %localappdata%\log =&gt; Logs from the debugging environment
  * %localappdata%\SDBADE =&gt; Data files \(databases, preferences, etc.\)
  * %appdata%\SDBADE =&gt; Configuration files

