# Applet Development Environment

The applet development environment is intended to provide developers of applets with an environment which mimics the dCDR applications such as the android, windows, linux, and gateway applications. The development environment provides the dCDR services and mimics:

* Offline synchronization with the central iCDR server
* Clinical Decision Support systems
* Business Rules execution
* Report and dataset rendering

Rather than relying on packaged and digitally signed applet files, the applet development environment will load source code directly from your hard drive and will simulate how the dCDR will operate on your files once packaged.

{% hint style="danger" %}
Never us the SDK environment to host a production instance of the SanteDB dCDR infrastructure. Use one of the production/release environments for your needs.&#x20;
{% endhint %}

## Console Options

**Tool: `sdb-ade.exe`**

The command line options for this tool are:

| Option   | Description                                                                                                                                                                                                                                                                                                                | Example                     |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| core     | Automatically reference the `org.santedb.core` solution.                                                                                                                                                                                                                                                                   | `--core`                    |
| solution | <p>References a solution file (see: <a href="../applet-solution-packages.md">Solutions</a>). The applet</p><p>development environment will scan subdirectories of the </p><p>applet for source code related to each applet package</p><p>contained in the solution. It should reference the </p><p>solution file.</p>      | `--solution=C:\temp\my.sln` |
| applet   | <p>Identifies applet package(s) which are being debugged. </p><p>The applet parameter loads only the specified applet</p><p>and may be used to side-load individual source code</p><p>into the debugging environment. It should reference a </p><p>directory with a <code>manifest.xml</code> which is being debugged.</p> | `--applet=C:\temp\app\`     |
| ref      | <p>References a pre-packaged applet either (1) installed</p><p>in the SDK installation directory, or (2) found on the </p><p>central SanteDB <a href="packaging-applets.md#package-repositories">package repository</a>.</p>                                                                                               | `--ref=org.santedb.core`    |
| reset    | <p>Clears the configuration for the current dCDR development<br>environment. This option allows you to "reset" your </p><p>development environment to match a fresh install of</p><p>the dCDR.</p>                                                                                                                         | `--reset`                   |
| name     | <p>Creates a segregated, named instance of the development</p><p>environment. This allows you to maintain <br>several configurations without resetting.</p>                                                                                                                                                                | `--name=MPI`                |
| assembly | <p>If you're writing a dCDR .NET plugin and wish to have</p><p>the SDK load your .NET plugin into the host context, </p><p>you can specify the assembly to load here.</p>                                                                                                                                                  | `--assembly=MyPlugin.dll`   |

### Named Instances

When you launch the applet debugging environment with no parameters, the configuration files are stored in the `%appdata%\sdbade\default` directory and offline synchronization data is stored in `%localappdata%\sdbade\default`, this is the DEFAULT instance of your debugging environment.

However, there are times when developers are working on several environments, and several servers at once. For example, it is quite possible that a developer would want to have an environment for development, an environment for staging server access and validation.&#x20;

In this case, the developer may launch their dCDR applet for development using:

```
> sdb-ade --ref=org.santedb.admin.sln --applet=C:\source\myapp --name=dev
```

When the developer needs to validate a bug/issue on a staging instance, he would simply switch configurations via:

```
> sdb-ade --ref=org.santedb.admin.sln --applet=C:\source\myapp --name=stage
```

When the developer does this, the existing configuration is applied as though he is using two different Android tablets, or gateway instances. Named instances store their data in `%localappdata%\sdbade\{name}` and configuration in `%appdata%\sdbade\{name}`.

{% hint style="info" %}
The disconnected gateway and the www host both support named instances as well.
{% endhint %}

