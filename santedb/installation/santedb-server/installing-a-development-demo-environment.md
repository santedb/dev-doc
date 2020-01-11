# Installing a Development / Demo Environment

If you'd like to give SanteDB a try, or if you're developing plugins for SanteDB you can use the quick configuration method. The quick configuration method will install SanteDB, register relevant services, open firewall ports, and install a sample dataset for a fake country called Elbonia.

{% hint style="info" %}
DO NOT use these instructions to deploy a production SanteDB environment. It leverages FirebirdSQL and assumes defaults for many of the configuration options. Production installation requires careful planning.
{% endhint %}

### Development Pre-Requisites

You'll need a machine \(or VM\) running Windows 8 Home Edition or better, with 2 GB of RAM and 1 CPU. 

You should use the latest SanteDB Server installer from : https://github.com/santedb/santedb-server/releases 

{% hint style="info" %}
You can install the development environment on Linux, however there is no bundled installer for this option. 
{% endhint %}

### Installing SanteDB Server

Launch the installer and accept the license agreement. By default the installer will not configure SanteDB or modify any security settings on the host environment. Because we want a quick development / demo environment we should select the "**Elbonia Quickstart"** option.

![Select the Elbonia Quickstart Option](../../../.gitbook/assets/image%20%2823%29.png)

After installation is completed, the SanteDB service will start and begin initialization of your sample dataset.

### Verify Installation

You can verify your installation by visiting: http://localhost:8080/api-docs in a web-browser.

![SanteDB&apos;s OpenAPI Documentation](../../../.gitbook/assets/image%20%284%29.png)

{% hint style="info" %}
You may receive a 503 - Service Unavailable error. This simply means SanteDB's service is not yet finished initializing your database. You can check the status of the installation in the log located at : C:\Program Files\SanteSuite\SanteDB\Server
{% endhint %}

### Access Credentials

SanteDB authenticates three types of principals on a session: User, Device, and Application. To get familiarized with the environment you can use the following credentials on this installation:

* User: Administrator
* Password: Mohawk123
* Client\_ID: fiddler
* Client\_Secret: fiddler
* Send client credentials in request body

