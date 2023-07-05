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
| certHash    | Specifies an X509 thumprint in your CurrentUser\My certificate store to use for signing                                                                                                                                                                 | --certHash=ABCDEF012345678    |
| info        | Displays the contents of the applet package file.                                                                                                                                                                                                       | --info                        |

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

The pakman tool can produce executable files native to the operating systems that the dCDR supports. By specifying the `--dcdr` parameter in conjunction with `--compose`, the pakman tool will produce branded assets.

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

## Inspecting Packages

{% hint style="info" %}
This section documents a SanteDB 3.0 Feature
{% endhint %}

The package manager can be used to inspect a packaged file (`.pak`) using the `--info` flag and specifying a source package. This command is useful for diagnosing package problems such as missing files, inappropriate embedded resources, etc.

The output of this command for a solution file is illustrated below:

```
> pakman --info --source=sln\santedb.admin.sln.pak
SanteDB HTML Applet Compiler v3.0.920.0 (Alberta)
Copyright (C) 2022 SanteSuite Inc. and the SanteSuite Contributors (See NOTICE.md)
Package Type: AppletSolution
Tooling Version: 2.2.1.10
ID: santedb.admin.sln
Version: 2.1.55.0
Author: SanteSuite Contributors
Name(s): SanteDB Administration
Public Key ID: 5A21255E8CA1A6938A3105AFF4EF9E82FAFD79B1
Content Hash: 20C5C2ACA8857BAC358F59B54520D88BF02E70FEDA3A6E35E9A2BBC0317818F3
Timestamp: 2023-07-04T15:26:12.1005879-04:00
=== Embedded Publisher Information ===
SN: CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
TUMB: 5A21255E8CA1A6938A3105AFF4EF9E82FAFD79B1
ISSUER: CN=SanteSuite Community Applet Code Signature CA, OU=SanteSuite Applet Code Signing, O=SanteSuite Community, S=ON, C=CA
VALIDITY: 2021-09-30 8:30:14 AM THRU 2023-09-30 8:30:14 AM
-- INCLUDES --
        1 - org.santedb.admin v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
        2 - org.santedb.core v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
        3 - org.santedb.uicore v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
        4 - org.santedb.bicore v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
        5 - org.santedb.config v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
        6 - org.santedb.config.init v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
        7 - org.santedb.i18n.en v. 2.5.12, CN=Fyfe Software Inc., O=Fyfe Software Inc., L=Hamilton, S=ON, C=CA
```

The output contains:

* Package Type: Indicating whether a package file contains a solution (AppletSolution) or a single package (AppletPackage)
* Tooling Version: Indicating the version of the SanteDB tooling which was used to create the package
* ID: The unique identifier for the package
* Version: The version of the package itself.
* Public Key ID: The thumbprint of the publisher's certificate used to sign the content
* Content Hash: The hash of the content which was signed with the issuing key
* Timestamp: The time that the package was created
* Embedded Publisher Information: If the `--embedcert` option was included on the command prompt, this is the certificate that was used by the publisher to sign the package.
