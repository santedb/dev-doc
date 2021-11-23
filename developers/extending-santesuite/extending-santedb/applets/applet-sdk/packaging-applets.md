# Package Manager

The applet compiler is a tool which will bundle your AngularJS controllers, views, models, business rules, protocols, reports, and other assets into a single compressed PAK file for distribution.

The applet compiler will also optionally sign the package using your signing key.

## Command Line Options

**Tool:** pakman.exe

The following parameters are supported by the applet compiler:

| Option      | Description                                                                                                                                                                                                                                             | Example                       |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| c           | Instructs the compiler to clean the output directory                                                                                                                                                                                                    |                               |
| source      | The source files / directory to include in the applet                                                                                                                                                                                                   | --source=c:\myapplet          |
| output      | The destination PAK file that should be created                                                                                                                                                                                                         | --output=myapplet.pak         |
| help        | Display application help and exit                                                                                                                                                                                                                       |                               |
| optimize    | When provided, instructs the applet compiler to minify javascript and css files                                                                                                                                                                         |                               |
| keyFile     | Specifies the location of your signing key (in PFX format)                                                                                                                                                                                              | --keyFile=mykey.pfx           |
| keyPassword | Specifies a file where the password to unlock your private key can be found                                                                                                                                                                             | --keyPassword=mykey.password  |
| compile     | Instructs the applet compiler to compile the --source directory into --output pak flie                                                                                                                                                                  |                               |
| sign        | Instructs the applet compiler to sign an exsiting --source pak file and output it to --output pak file                                                                                                                                                  |                               |
| embedCert   | Instructs the applet compiler to embed a copy of the public key into the PAK file (recommended for deployments)                                                                                                                                         |                               |
| compression | Changes the compression algorithm from DEFLATE to an alternate method (lzma, gzip, bzip2, defalte)                                                                                                                                                      | --compression=lzma            |
| compose     | If your manifest file is an applet solution (a bundle of other applets), then this command will compose the solution pak file.                                                                                                                          | --compose=mysln.xml           |
| install     | Instructs the pakman tool to place the output file into its reference cache.                                                                                                                                                                            | --install                     |
| dcdr        | <p>Instructs the pakman tool to create a branded SanteDB executable assets. Options:</p><ul><li>android = Android APK</li><li>gateway = dCDR Gateway Installer</li><li>windows = dCDR Windows UI Installer</li><li>web = Web Portal Installer</li></ul> | --dcdr=android --dcdr=gateway |
| msbuild     | Specifies the path to the MSBuild instance you want to use. (By default the tool will scan your C:\Program Files\Microsoft Visual Studio\\\* directory for an MSBuild executable)                                                                       | --msbuild="path"              |

## **Packaging your Applet**

**Creating an Unsigned Applet (Debugging Only)**

To create an unsigned applet:

1. Ensure your manifest.xml file is accurate including version, package id, etc.
2.  Run the applet compiler as follows:

    ```
     pakman --source=C:\myapp --output=myapp.pak
    ```
3. Upload myapp.pak to your SanteDB HDS server
4. Join your SanteDB HDS server with the disconnected client
   1. Your HDS server may not start or may refuse to load unsigned applets. If this is the case either configure your IMS server to allow unsigned applets or sign your applet&#x20;
   2. Notice that your disconnected client will warn you that the package is not signed
   3. Note that contents of the file can be accessed by using `sdb-dcc --debug` , no minifcation has occurred.

**Creating a Production Applet**

To create a production (optimized) applet:

1. Ensure your manifest.xml file is accurate including version, packagte id, etc.
2.  Run the applet compiler as follows:

    ```
     pakman --source=C:\myapp --output=myapp.pak --optimize --keyFile=C:\keys\mykey.pfx --embedCert
    ```
3. When prompted enter the private key password for your PFX file 1. Alternately you can save the password in a file and use --keyPassword parameter (make sure the key password file and PFX file are kept out of source control)
4. Upload myapp.pak to your SanteDB HDS server
5. Join your SanteDB HDS server with the disconnected client
   1. Your IMS server may not start or may refuse to applets signed from third party keys. If this is the case add the thumbprint of your signing key to \<trustedPublishers>
   2. The disconnected client may warn that the application is from an unknown publisher
   3. Note that contents of the controller files are minified, so running `sdb-ade` will require un-minification tools to debug.

## Bundling Branded dCDR Assets

The pakman tool can produce executable files native to the operating systems that the dCDR supports. By specifying the `--dcdr `parameter in conjunction with `--compose`, the pakman tool will produce branded assets.

### Android APK

To have the pakman tool generate a branded dCDR Android app, use the `--dcdr=android` option, the requirements for building an android APK are:

* Microsoft Visual Studio 2017 Community or higher
  * Xamarin / Android Mobile Development option enabled
* Pakman version 2.0.25 or higher.

The command to compose an android APK is:

```markup
pakman --compose --dcdr=android --source=org.sample.santedb.sln.xml 
          --output=.\dist\org.sample.santedb.pak
          --keyFile=<path to PFX>
          --embedCert
```

The APK will be placed in the same output directory as the solution pak file.

#### Manifest Data

The android manifest for the APK is generated from the manifest.xml file in your solution which was composed. For example, given the following solution manifest

```markup
<AppletManifest xmlns="http://santedb.org/applet">
  <info id="org.santedb.sample.sln" version="2.0.33.0">
    <icon>/org.santedb.sample/img/logo.png</icon>
    <name lang="en">My Registration Application</name>
    <author>SanteDB</author>
    <dependency id="org.santedb.sample.sln" version="2.0.33.0"/>
    <dependency id="org.santedb.core" version="2.0.33.0"/>
    <dependency id="org.santedb.config" version="2.0.33.0"/>
    <dependency id="org.santedb.i18n.en" version="2.0.33.0"/>
  </info>

</AppletManifest>
```

Will produce an APK with:

|                                             |                              |
| ------------------------------------------- | ---------------------------- |
| packageId                                   | org.santedb.sample.sln       |
| versionCode                                 | 2.0.33.0                     |
| name (on the Android home screen)           | My Registration Application  |
| icon (on the splash screen and home screen) | /org.santedb.sample/logo.png |

The APK will be bundled with the packages listed as dependencies on the solution.&#x20;

## Publishing Your Applet

In order to publish your applet, you must first acquire a code signing certificate signed by the SanteDB community. If you don't have a code signing certificate your organization can obtain one by becoming a registered community contributor.

See the [SanteDB Software Publishers ](../../../../santedb-software-publishers/)page for more information.

## Package Repositories

The PakMan tool will pull solution dependencies when the --compose option is used from the following sources:

* The local cache of packages&#x20;
  * On Windows : %localappdata%\\.santedb-sdk&#x20;
  * On Unix : \~/.local/.santedb-sdk
* Any configured external repositories in the pakman.config file
  * On Windows : %appdata%\santedb\sdk
  * On Unix: \~/.config/santedb/sdk

Repositories can be local (for development) or remote (for production).

### Repository Configuration

To configure the package repository edit/create the pakman.config file in the appropriate configuration directory, for example, to configure the master repository at https://packages.santesuite.net :

```markup
<?xml version="1.0"?>
<PakManConfig xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/pakman">
  <repositories>
    <add>file://~/dev-repo</add>
  	<add>https://packages.santesuite.net</add>
  </repositories>
</PakManConfig>
```

### Publishing to a Repository

To publish to a repository you will need to obtain a publisher credential. You should then add this credential to your configuration file:

```markup
<add username="myser" password="MyPassword">https://packages.santesuite.net</add>
```

When packaging your applet you will specify the publish option:

```markup
pakman --compile --source=~/myproject --optimize --keyFile=XXXXX --embedCert
       --output=~/myproject/.bin/myproject.pak --publish --publish-server=URL
```

This will package your application and then push the packaged application to the remote repository.
