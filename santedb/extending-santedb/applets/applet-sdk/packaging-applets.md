# Package Manager

The applet compiler is a tool which will bundle your AngularJS controllers, views, models, business rules, protocols, reports, and other assets into a single compressed PAK file for distribution.

The applet compiler will also optionally sign the package using your signing key.

## Command Line Options

**Tool:** pakman.exe

The following parameters are supported by the applet compiler:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">c</td>
      <td style="text-align:left">Instructs the compiler to clean the output directory</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">source</td>
      <td style="text-align:left">The source files / directory to include in the applet</td>
      <td style="text-align:left">--source=c:\myapplet</td>
    </tr>
    <tr>
      <td style="text-align:left">output</td>
      <td style="text-align:left">The destination PAK file that should be created</td>
      <td style="text-align:left">--output=myapplet.pak</td>
    </tr>
    <tr>
      <td style="text-align:left">help</td>
      <td style="text-align:left">Display application help and exit</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">optimize</td>
      <td style="text-align:left">When provided, instructs the applet compiler to minify javascript and
        css files</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">keyFile</td>
      <td style="text-align:left">Specifies the location of your signing key (in PFX format)</td>
      <td style="text-align:left">--keyFile=mykey.pfx</td>
    </tr>
    <tr>
      <td style="text-align:left">keyPassword</td>
      <td style="text-align:left">Specifies a file where the password to unlock your private key can be
        found</td>
      <td style="text-align:left">--keyPassword=mykey.password</td>
    </tr>
    <tr>
      <td style="text-align:left">compile</td>
      <td style="text-align:left">Instructs the applet compiler to compile the --source directory into --output
        pak flie</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">sign</td>
      <td style="text-align:left">Instructs the applet compiler to sign an exsiting --source pak file and
        output it to --output pak file</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">embedCert</td>
      <td style="text-align:left">Instructs the applet compiler to embed a copy of the public key into the
        PAK file (recommended for deployments)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">compression</td>
      <td style="text-align:left">Changes the compression algorithm from DEFLATE to an alternate method
        (lzma, gzip, bzip2, defalte)</td>
      <td style="text-align:left">--compression=lzma</td>
    </tr>
    <tr>
      <td style="text-align:left">compose</td>
      <td style="text-align:left">If your manifest file is an applet solution (a bundle of other applets),
        then this command will compose the solution pak file.</td>
      <td style="text-align:left">--compose=mysln.xml</td>
    </tr>
    <tr>
      <td style="text-align:left">install</td>
      <td style="text-align:left">Instructs the pakman tool to place the output file into its reference
        cache.</td>
      <td style="text-align:left">--install</td>
    </tr>
    <tr>
      <td style="text-align:left">dcdr</td>
      <td style="text-align:left">
        <p>Instructs the pakman tool to create a branded SanteDB executable assets.
          Options:</p>
        <ul>
          <li>android = Android APK</li>
          <li>gateway = dCDR Gateway Installer</li>
          <li>windows = dCDR Windows UI Installer</li>
          <li>web = Web Portal Installer</li>
        </ul>
      </td>
      <td style="text-align:left">--dcdr=android --dcdr=gateway</td>
    </tr>
    <tr>
      <td style="text-align:left">msbuild</td>
      <td style="text-align:left">Specifies the path to the MSBuild instance you want to use. (By default
        the tool will scan your C:\Program Files\Microsoft Visual Studio\* directory
        for an MSBuild executable)</td>
      <td style="text-align:left">--msbuild=&quot;path&quot;</td>
    </tr>
  </tbody>
</table>

## **Packaging your Applet**

**Creating an Unsigned Applet \(Debugging Only\)**

To create an unsigned applet:

1. Ensure your manifest.xml file is accurate including version, package id, etc.
2. Run the applet compiler as follows:

   ```text
    pakman --source=C:\myapp --output=myapp.pak
   ```

3. Upload myapp.pak to your SanteDB HDS server
4. Join your SanteDB HDS server with the disconnected client
   1. Your HDS server may not start or may refuse to load unsigned applets. If this is the case either configure your IMS server to allow unsigned applets or sign your applet 
   2. Notice that your disconnected client will warn you that the package is not signed
   3. Note that contents of the file can be accessed by using `sdb-dcc --debug` , no minifcation has occurred.

**Creating a Production Applet**

To create a production \(optimized\) applet:

1. Ensure your manifest.xml file is accurate including version, packagte id, etc.
2. Run the applet compiler as follows:

   ```text
    pakman --source=C:\myapp --output=myapp.pak --optimize --keyFile=C:\keys\mykey.pfx --embedCert
   ```

3. When prompted enter the private key password for your PFX file 1. Alternately you can save the password in a file and use --keyPassword parameter \(make sure the key password file and PFX file are kept out of source control\)
4. Upload myapp.pak to your SanteDB HDS server
5. Join your SanteDB HDS server with the disconnected client
   1. Your IMS server may not start or may refuse to applets signed from third party keys. If this is the case add the thumbprint of your signing key to &lt;trustedPublishers&gt;
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

|  |  |
| :--- | :--- |
| packageId | org.santedb.sample.sln |
| versionCode | 2.0.33.0 |
| name \(on the Android home screen\) | My Registration Application |
| icon \(on the splash screen and home screen\) | /org.santedb.sample/logo.png |

The APK will be bundled with the packages listed as dependencies on the solution. 

## Publishing Your Applet

In order to publish your applet, you must first acquire a code signing certificate signed by the SanteDB community. If you don't have a code signing certificate your organization can obtain one by becoming a registered community contributor.

See the [SanteDB Software Publishers ](../../../santedb/santedb-software-publishers.md)page for more information.

## Package Repositories

The PakMan tool will pull solution dependencies when the --compose option is used from the following sources:

* The local cache of packages 
  * On Windows : %localappdata%\.santedb-sdk 
  * On Unix : ~/.local/.santedb-sdk
* Any configured external repositories in the pakman.config file
  * On Windows : %appdata%\santedb\sdk
  * On Unix: ~/.config/santedb/sdk

Repositories can be local \(for development\) or remote \(for production\).

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

