# Applet Solution Packages

Applet solution packages allow developers to bundle together a series of individual applet PAK files into a single file. There are a variety of reasons you may want to do this:

* It ensures that any dependencies your applet requires are present on the target system when the solution is deployed.
* It allows one single SanteDB deployment to support multiple user interfaces which can be selectively subscribed to by clients.
* It prevents tampering by allowing the bundling of a single pak file which is signed with your publishing key and verified at startup in the SanteDB service.

Applet solution packages are described using a solution XML file and composed from a series of PAK files. The process for compiling and creating an applet solution is simple:

1. Write your applet like you normally would 
2. Create a package manifest file 
3. Compile your applets \(see Packaging Applets\)
4. Compose the applet packages into a single solution file

### Solution Manifest

An applet solution manifest is really just a point to other applets which are composed. The format of the solution manifest is illustrated below:

```markup
<AppletManifest xmlns="http://santedb.org/applet">
  <info id="santedb.sample.sln" version="1.0.0.0">
    <icon>/org.santedb.core/img/icon.png</icon>
    <name lang="en">SanteDB Sample</name>
    <author>SanteSuite Contributors</author>
    <dependency id="org.santedb.core" version="1.46.0.0"/>
    <dependency id="org.santedb.uicore" version="1.46.0.0"/>
    <dependency id="org.santedb.bicore" version="1.46.0.0"/>
    <dependency id="org.santedb.config" version="1.46.0.0"/>
    <dependency id="org.santedb.config.init" version="1.46.0.0"/>
    <dependency id="org.santedb.i18n.en" version="1.46.0.0"/>
    <dependency id="org.santedb.sample" version="1.0.0.0"/>
  </info>
</AppletManifest>
```

In this example, only the org.santedb.sample package needs to be written, the rest of the applets would simply need their pak files in the directory while composing.

### Composing your Solution

Once you are ready to distribute your applet solution you use the sdb-pakr command \(the same as used to package your applet\). 

```markup
sdb-pakr --compile --source=.\ -o org.santedb.sample.pak
sdb-pakr --compose --source=santedb.sample.sln.xml -o santedb.sample.sln.pak
```

The generated pak file contains static copies of the referenced pak files as well as a package manifest.

