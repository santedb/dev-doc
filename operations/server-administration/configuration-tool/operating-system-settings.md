# Operating System Settings

The operating system settings panel controls SanteDB iCDR's interaction with the host operating system.

## Windows Service

The Windows Service configuration panel allows for the configuration of the Windows Service Manager (`services.msc`) registration. This is what allows SanteDB to auto-start on Microsoft Windows Operating Systems.

![](<../../../.gitbook/assets/image (725).png>)

<table><thead><tr><th width="216.2676612932232">Setting</th><th width="269.5026452105254">Description</th><th>Values</th></tr></thead><tbody><tr><td>Instance Name</td><td>When running SanteDB with multiple named instances on the same server, this sets the instance name of the service which is registered in the Windows Service Manager. Each named instance may carry its own configuration file.</td><td>String</td></tr><tr><td>Service Account</td><td>By default SanteDB runs as LOCAL SERVICE , however you can specify an alternate service account you'd like to run SanteDB under. This is recommended if you're running SanteDB in an environment where it needs to access network resources such as storing match configurations on a UNC network share.</td><td>Windows Account Name</td></tr><tr><td>Service Account Password</td><td>The password for the entered service account.</td><td></td></tr><tr><td>Startup Behavior</td><td>Controls the startup behavior of the SanteDB service. Default is AutoStart</td><td><p>AutoStart = Started when Windows Starts</p><p>Start = Manually Started</p><p>Disabled = Never Start (prevent running)</p></td></tr></tbody></table>
