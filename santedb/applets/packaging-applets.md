# Packaging Applets

The applet compiler is a tool which will bundle your AngularJS controllers, views, models, business rules, protocols, reports, and other assets into a single compressed PAK file for distribution.

The applet compiler will also optionally sign the package using your signing key.

## Command Line Options

**Tool:** sdb-pakr.exe

The following parameters are supported by the applet compiler:

| Option | Description | Example |
| :--- | :--- | :--- |
| deploy | Deploys the rendered applet files to an HTTP server location | --deploy=/srv/www/htdocs |
| lang | The language to pre-render deployed output files in | --lang=en |
| c | Instructs the compiler to clean the output directory |  |
| source | The source files / directory to include in the applet | --source=c:\myapplet |
| output | The destination PAK file that should be created | --output=myapplet.pak |
| help | Display application help and exit |  |
| include | Includes / references files from another applet pak file | --include=org.santedb.core.pak |
| optimize | When provided, instructs the applet compiler to minify javascript and css files |  |
| keyFile | Specifies the location of your signing key \(in PFX format\) | --keyFile=mykey.pfx |
| keyPassword | Specifies a file where the password to unlock your private key can be found | --keyPassword=mykey.password |
| compile | Instructs the applet compiler to compile the --source directory into --output pak flie |  |
| sign | Instructs the applet compiler to sign an exsiting --source pak file and output it to --output pak file |  |
| embedCert | Instructs the applet compiler to embed a copy of the public key into the PAK file \(recommended for deployments\) |  |
| compression | Changes the compression algorithm from DEFLATE to an alternate method \(lzma, gzip, bzip2, defalte\) | --compression=lzma |
| compose | If your manifest file is an applet solution \(a bundle of other applets\), then this command will compose the solution pak file. | --compose=mysln.xml |

## **Packaging your Applet**

**Creating an Unsigned Applet \(Debugging Only\)**

To create an unsigned applet:

1. Ensure your manifest.xml file is accurate including version, package id, etc.
2. Run the applet compiler as follows:

   ```text
    sdb-pakr --source=C:\myapp --output=myapp.pak
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
    sdb-pakr --source=C:\myapp --output=myapp.pak --optimize --keyFile=C:\keys\mykey.pfx --embedCert
   ```

3. When prompted enter the private key password for your PFX file 1. Alternately you can save the password in a file and use --keyPassword parameter \(make sure the key password file and PFX file are kept out of source control\)
4. Upload myapp.pak to your SanteDB HDS server
5. Join your SanteDB HDS server with the disconnected client
   1. Your IMS server may not start or may refuse to applets signed from third party keys. If this is the case add the thumbprint of your signing key to &lt;trustedPublishers&gt;
   2. The disconnected client may warn that the application is from an unknown publisher
   3. Note that contents of the controller files are minified, so running `sdb-dcc --debug` will require un-minification tools to debug.

## Publishing Your Applet

In order to publish your applet, you must first acquire a code signing certificate signed by the SanteDB community. If you don't have a code signing certificate your organization can obtain one following this process:

1. Create a certificate signing request \(CSR\) for your organization \(if you don't want to do this the community can issue a PFX with a custom private key\).
2. Visit the SanteSuite developer's community page and complete the **Request Community Signing Certificate** form. Include your CSR generated in step 1.  The community usually verifies:
   1. Your organization has not been blacklisted previously \(for circumventing community rules\)
   2. Your organization is a recognized community partner which contributes in some manner, to the community.
   3. Your organization has a web-presence and/or contact person.
3. After a brief period, the community will issue your organization a 1 year code signing certificate file \(in PFX form\) which can be used to sign your applets.
4. When your signing certificate is about to expire, you can renew it.

After acquiring the PFX signed by the community you can use the --sign option to compile your applet in a release mode. This will sign your package so it can be downloaded and loaded into any stock SanteDB project. If you would like to deploy your applet to the community applet store \(to be more widely accessible\) you will need to follow these additional steps:

1. Visit the SanteSuite applet store and submit a new package.
2. Attach your signed PAK file to the package submission form.
3. The SanteDB community will verify your applet as soon as possible, the community members check for:
   1. Your applet follows the appropriate user interface standards and operates on all platforms SanteDB runs on.
   2. Your applet does not cause or does not contain unnecessary/inappropriate API calls \(for example, deleting all users and/or changing passwords when loaded, etc.\)
   3. Your organization is in good standing with the community.
4. If the community reviewers are satisfied your applet meets the criteria, the community will provide a secondary signature \(SanteDB VERIFIED Signature\) to the PAK file and will upload the PAK to the SanteSuite applet store. 

