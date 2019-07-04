---
description: >-
  This page describes the necessary steps to configure the SanteDB Server
  instance.
---

# Configuration

## Guided Configuration

If you installed SanteDB Server on a server running Microsoft Windows,you can choose to install the necessary services using the built-in configuration tool. The configuration tool is launched after setup. 

When you first launch the configuration tool, you will be presented with two options:

1. **Easy Configuration:** Which automatically sets up most of the SanteDB services with the default options.
2. **Advanced Configuration:** Which does not configure any services, and provides you with an opportunity to manually configure only the features you wish.

![Figure 1 - Initial Configuration Screen](../../../.gitbook/assets/image%20%2812%29.png)

### Easy Configuration Walkthrough

#### Database Settings

Using the Easy Configuration option, you will be asked to select **Database Software.** By default, there are two options for PostgreSQL or FirebirdSQL. When you select the database software option, you will be prompted with configuration parameters for that particular RDBMS. 

The tooling will also provide you with an opportunity to create a new database \(SDB\_BASE.FDB is the default sample database\).

![Figure 2 - Database Connection Properties](../../../.gitbook/assets/image%20%283%29.png)

When selecting **New...** you will be presented with an opportunity to specify the name of your new database:

![Figure 3 - Creating a new Database](../../../.gitbook/assets/image%20%288%29.png)

#### Instance Name

The last setting you may wish to modify is the "Instance Name". Instance naming allows multiple SanteDB Server instances running on the same machine to operate on different ports. This is useful for demonstrations or shared hosing environments. Leaving this to the default **SanteDB** is ideal if you only plan on running one instance of SanteDB Server on the machine.

#### Executing Initial Setup Tasks

When you press **Continue** on the initial configuration page, you will be presented with a list of tasks which will be executed in order to configure your instance of SanteDB Server. This window allows you to bypass any configuration steps you don't want performed \(such as updates, demonstration data, etc.\). For example, if I didn't want the configuration tool to install SanteDB Server as a windows service \(perhaps I only want to run the server on the console\), I could disable that particular task.

![Figure 4 - Disabling A Task](../../../.gitbook/assets/image%20%2811%29.png)

Once you have pressed OK, you will be shown the status of configuration: 

![Figure 5 - Configuration Worker](../../../.gitbook/assets/image%20%2820%29.png)

#### Importing Default Datasets

After the initial configuration screen has completed, you will be prompted to confirm a series of tasks which will import the default data sets into SanteDB. 

{% hint style="info" %}
On FirebirdSQL you may receive "Connection Shutdown", this is an internal FirebirdSQL server fault and we are actively working to fix it. Until then, you can simply restart the configuration program and the import will continue.
{% endhint %}

![Figure 6 - Secondary Configuration Tasks](../../../.gitbook/assets/image%20%2826%29.png)

The installation of the initial datasets for your SanteDB deployment may take some time, this is normal.

![Figure 7 - Import of Initial Data](../../../.gitbook/assets/image%20%282%29.png)



