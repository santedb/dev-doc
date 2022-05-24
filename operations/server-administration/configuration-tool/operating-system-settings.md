# Operating System Settings

The operating system settings panel controls SanteDB iCDR's interaction with the host operating system.

## Windows Service

The Windows Service configuration panel allows for the configuration of the Windows Service Manager (`services.msc`) registration. This is what allows SanteDB to auto-start on Microsoft Windows Operating Systems.

![](<../../../.gitbook/assets/image (419) (1) (1) (1) (1).png>)

| Setting                  | Description                                                                                                                                                                                                                                                                                              | Values                                                                                                                       |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Instance Name            | When running SanteDB with multiple named instances on the same server, this sets the instance name of the service which is registered in the Windows Service Manager. Each named instance may carry its own configuration file.                                                                          | String                                                                                                                       |
| Service Account          | By default SanteDB runs as LOCAL SERVICE , however you can specify an alternate service account you'd like to run SanteDB under. This is recommended if you're running SanteDB in an environment where it needs to access network resources such as storing match configurations on a UNC network share. | Windows Account Name                                                                                                         |
| Service Account Password | The password for the entered service account.                                                                                                                                                                                                                                                            |                                                                                                                              |
| Startup Behavior         | Controls the startup behavior of the SanteDB service. Default is AutoStart                                                                                                                                                                                                                               | <p>AutoStart = Started when Windows Starts</p><p>Start = Manually Started</p><p>Disabled = Never Start (prevent running)</p> |
