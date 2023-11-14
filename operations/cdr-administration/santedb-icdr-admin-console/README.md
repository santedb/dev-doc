# SanteDB Administration Console

The SanteDB iCDR administrative console is a client tool which allows system administrators to quickly manage their iCDR instances from a command line. This tool is useful when:

* Internet connectivity is extremely limited and text interface is preferred
* You need to save output/reports for administrative functions to files
* You have not yet setup the web-based administrative portal

## Starting the Console

You can launch the command line on the same machine as the iCDR service from the start menu or by typing the `sdbac` command in the command line. If you need to connect to a different server/realm the basic syntax is:

```
sdbac --realm=<server-ip-or-name> --port=<port> [--tls] 
```

The command line options for sdbac are listed below:

| Short | Long          | Description                                                                                                                                            |
| ----- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| -r    | --realm       | The server/realm to which you're connecting.                                                                                                           |
| -a    | --appId       | <p>The application identifier if the default administrative console application</p><p>has not been enabled by the system administrator.</p>            |
| -s    | --secret      | The application secret if the default has been changed by the administrator                                                                            |
|       | --port        | The port to connect to the iCDR API on                                                                                                                 |
| -t    | --tls         | <p>If specified, instruct the console administrative application to connect</p><p>via TLS</p>                                                          |
| -u    | --user        | The username to login with                                                                                                                             |
| -p    | --password    | The password to use for authentication                                                                                                                 |
| -v    | --verbose     | When present, output all server and client events with full stack traces                                                                               |
| -x    | --proxy       | When specified route all traffic through a proxy                                                                                                       |
| -b    | --oauth-basic | <p>When specified, instructs the client to send client credentials via HTTP BASIC</p><p>rather than through the request body of the OAUTH request.</p> |

## Getting Help

You can run the help command in order to get a list of commands which are available on the administrative console.&#x20;

```
> help
aa.add              Add Assigning Authority application
aa.list             Query assigning authorties/identity domains
applet.download     Download the applet
applet.list         Lists all applets installed on the server
application.add     Add security application
application.del     De-activates an application in the SanteDB instance
application.info    Displays detailed information about the application
application.list    List Security Applications
application.lock    Engages or disengages the application lock
application.undel   Re-activates an application in the SanteDB instance
cdr.query           Query data from CDR
clear               Clears the screen
device.add          Add security device
device.alter        Alter security device
device.del          De-activates a device in the SanteDB instance
device.info         Displays detailed information about the device
device.list         List Security Devices
device.lock         Engages or disengages the device lock
device.undel        Re-activates a device in the SanteDB instance
exit                Quits the administrative shell
help                Shows help
log.cat             Lists the contents of the specified file
log.list            Lists the available log files
log.messages        Outputs the most recent log file
policy.assign       Assign security policies to objects
policy.list         List security policies
role.add            Adds a role to the current SanteDB instance
role.info           Displays detailed information about the role
role.list           List Security Roles
server.asm          Shows the server assembly information
server.info         Gets diagnostic information from the server
server.services     Shows the server service information
server.threads      Shows the server thread information
user.add            Adds a user to the SanteDB instance
user.del            De-activates a user to the SanteDB instance
user.info           Displays detailed information about the user
user.list           Lists users in the SanteDB instance
user.lock           Engages or disengages the user lock
user.password       Changes a users password
user.roles          Change roles for a user
user.undel          Re-activates a user to the SanteDB instance
ver                 Shows current Admin Console Version
whoami              Identifies the current authentication principal
Use:
        help cmd
For command specific help
```

If you require help for a specific command use the `help command` syntax, for example, to get help with user.list:

```
> help user.list
user.list parms - Lists users in the SanteDB instance
           + This command lists all users in the user database regardless of their status, or class. To filter use the filter parameters listed.
 -l                 Filter on locked status
 -a                 Show obsolete non-active status
 -h                 Filter on human class only
 -s                 Filter on system class only
 -u                 The username of the user
```

## Topics

{% content-ref url="user-administration.md" %}
[user-administration.md](user-administration.md)
{% endcontent-ref %}

{% content-ref url="group-role-management.md" %}
[group-role-management.md](group-role-management.md)
{% endcontent-ref %}

{% content-ref url="policy-administration.md" %}
[policy-administration.md](policy-administration.md)
{% endcontent-ref %}

{% content-ref url="untitled.md" %}
[untitled.md](untitled.md)
{% endcontent-ref %}

{% content-ref url="application-administration.md" %}
[application-administration.md](application-administration.md)
{% endcontent-ref %}

