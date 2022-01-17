# Quick Start Guide

This tutorial will provide an overview of how to install and run the SanteDB iCDR MPI solution (SanteMPI) using Docker for a demonstration environment.

{% hint style="info" %}
Do not use these instructions to deploy SanteMPI in a production environment. These instructions are intended to provide a quick start for demonstration or evaluation only.&#x20;
{% endhint %}

{% hint style="info" %}
The code for the quick-start guide can be found on the SanteDB GitHub page at: [https://github.com/santedb/hello-mpi](https://github.com/santedb/hello-mpi)
{% endhint %}

## Pre-Requisites

This tutorial uses Docker as a basis for illustrating SanteMPI functions. In order to complete this tutorial, users should:

* Have Docker installed on the host system (on Windows or Linux)
* Have a text editor which can be used to edit the docker YML files
* Installed SOAP UI ([https://www.soapui.org/downloads/latest-release/](https://www.soapui.org/downloads/latest-release/))
* Downloaded the Installation Qualification Test Suite ([https://github.com/santedb/santempi/blob/master/SanteMPI-Test-Cases-soapui-project.xml](https://github.com/santedb/santempi/blob/master/SanteMPI-Test-Cases-soapui-project.xml))

## Create the Docker Application

In a text editor, create a new directory and create a new text file called `docker-compose.yml` in that directory.

```
mkdir quickstart
notepad docker-compose.yml
```

First, you will need to create a postgresql service, this is where the SanteMPI database will be stored.

```yaml
version: "3.3"

services:
  db:
    image: postgres
    container_name: sdb-postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: santedb
      POSTGRES_PASSWORD: SanteDB123
    restart: always

```

This section:

* Creates a new docker service called `db` from the `postgres:latest` tag
* Exposes the PostgreSQL database on the host on port 5432
* Sets the initial postgresql user to `santedb` with password `SanteDB123`

Next, declare the `santedb-mpi` service , this service will host the the actual iCDR which has SanteMPI:

```yaml
  santedb:
    image: santesuite/santedb-mpi:latest
    container_name: santedb-mpi
    environment:
      - SDB_FEATURE=LOG;DATA_POLICY;AUDIT_REPO;ADO;PUBSUB_ADO;RAMCACHE;SEC;SWAGGER;OPENID;FHIR;FHIR_AUDIT;HL7;HDSI;AMI;BIS;MDM;MATCHING;IHE_PIXM;IHE_PDQM;IHE_PMIR;IHE_PIX;IHE_PDQ
      - SDB_HL7_AUTHENTICATION=Msh8
      - SDB_MATCHING_MODE=WEIGHTED
      - SDB_MDM_RESOURCE=Patient
      - SDB_MDM_AUTO_MERGE=false
      - SDB_DB_MAIN=server=sdb-postgres;port=5432; database=santedb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_AUDIT=server=sdb-postgres;port=5432; database=auditdb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_MAIN_PROVIDER=Npgsql
      - SDB_DB_AUDIT_PROVIDER=Npgsql
      - SDB_DATA_POLICY_ACTION=HIDE
      - SDB_DELAY_START=5000
    ports:
      - "8080:8080"
      - "2100:2100"
    depends_on:
      - db
    restart: always
```

This section of the file:

* Creates a service named `santedb-mpi` in the docker environment
* Enables feature via the `SDB_FEATURE` environment variable (for reference see: [feature-configuration.md](installation-1/santedb-server/installation-using-appliances/docker-containers/feature-configuration.md "mention")
* Instructs the iCDR to enable [master-data-storage.md](../santedb/data-and-information-architecture/data-storage-patterns/master-data-storage.md "mention") for `Patient` resources
* Connects the main database to `santedb` on the `db` container.
* Connects the audit database to `auditdb` on the db container
* Instructs the iCDR to `hide` any data which is tagged with a privacy policy (other options are `redact`, `audit, none`
* Instructs the iCDR to wait 5 seconds before starting (to allow the database to initialize)
* Forward/expose the iCDR APIs on port 8080

Finally, create a container which will run the web access gateway using `santedb-www:latest`

```yaml
  www:
    image: santesuite/santedb-www:latest
    container_name: santedb-www
    ports:
      - "9200:9200"
    depends_on:
      - santedb
    restart: alwaysyaml
```

This section:

* Creates a service named `www` which uses the `santedb-www` image
* Forward traffic to the web portal on port 9200

## Start the Docker Application

After saving the text file, return to your command prompt and type:

```
docker compose -f docker-compose.yml up
```

This will start the SanteDB iCDR (running SanteMPI), the web access gateway and database. Initial startup of the SanteMPI container can take upwards of 5 minutes. You will see a log entry which indicates that startup was successful after this time.

## Configure the Web Access Gateway

You can now configure the web-access gateway, the [Configuring the Web Access Gateway ](installation-1/disconnected-gateway/installing-web-access-gateway.md#configure-the-web-access-gateway)article contains detailed instructions on how this is performed.&#x20;

### Join the Realm

Once startup is completed, navigate to [http://127.0.0.1:9200](http://127.0.0.1:9200) in your web browser. You will be prompted for connection details. For the quick start use:

* Device ID: quick-web
* Realm: santedb-mpi

The rest of the settings can be left as their defaults.

![](<../.gitbook/assets/image (427) (1) (1).png>)

Pressing the `Join` button will prompt you for a user name and password, use `Administrator` and `Mohawk123` as the password.

![](<../.gitbook/assets/image (422) (1) (1).png>)

### Select the MPI Role

You will be managing a SanteMPI server, therefore you will need to instruct the web access gateway that this gateway will be acting in the "SanteDB Master Patient Index Functions" solution.

![](<../.gitbook/assets/image (420).png>)

{% hint style="info" %}
Ensure you select the option to automatically download updates for applet files. This will ensure new applets uploaded to the iCDR will be downloaded by the dCDR gateway.
{% endhint %}

### Set Online Only Function Level

Since the web access gateway will be acting as an administration panel, you should set the dCDR in online only mode (no disconnected use)\


![](<../.gitbook/assets/image (433) (1) (1) (1) (1).png>)

{% hint style="danger" %}
The `santedb-www` and Web Access Gateway in general lack the SQLite binaries needed to operate in offline mode. If you select offline mode your web container will most likely not start up.
{% endhint %}

### Accept Defaults

You can accept the defaults for the following screens:

* Logging - This screen sets the verbosity of the output to your Docker host log
* Application Services - This screen allows for the enabling of third party or additional services which are not required by the web access gateway.
* Network - This screen allows you to configure the optimization between the dCDR and iCDR

Full documentation of these settings can be found on the [installing-web-access-gateway.md](installation-1/disconnected-gateway/installing-web-access-gateway.md "mention") and [installing-disconnected-gateway.md](installation-1/disconnected-gateway/installing-disconnected-gateway.md "mention") wiki articles.

### Customize the User Interface

You can customize the manner in which the SanteMPI user interface behaves by setting one or more [app-settings.md](installation-1/disconnected-gateway/app-settings.md "mention"). For example, the configuration below will only require given and family names to be registered, and will show the normally hidden fields for collecting patient Religion.

&#x20;

![](<../.gitbook/assets/image (418) (1).png>)

### Wait for Refresh

Once your settings are saved, the web access gateway will save the settings and restart itself.

![](<../.gitbook/assets/image (426) (1).png>)

## Customize the MPI

You can now log into the web administration console for the Master Patient Index. You can use the administrator/Mohawk123 account to log into the administrative panel.

![](<../.gitbook/assets/image (447) (1) (1).png>)

{% hint style="info" %}
Full documentation for the Administrative panel is available at the [Broken link](broken-reference "mention") page.
{% endhint %}

### Give Administrators Access to MDM and Clinical Data

Since this is a demonstration environment, you will probably want to change the default access policies for `Administrators` to allow them to see clinical data and perform MDM tasks. This is done by navigating to `Security -> Groups` and pressing edit on the `Administrators` group.

![](<../.gitbook/assets/image (421) (1) (1).png>)

You can scroll to `Policies` and add the following policies to the group:

* Unrestricted MDM
* Unrestricted Clinical Data

![](<../.gitbook/assets/image (446) (1).png>)

After adding these policies you should observe the policies in the master list of permissions.

![](<../.gitbook/assets/image (434) (1) (1) (1) (1).png>)

{% hint style="info" %}
You do not need to SAVE policy assignments, they are applied immediately.
{% endhint %}

### Re-Authenticate

The policies associated with your session for Administrator were established when you logged in, you've changed the policy set, however, your session will still have the old policy assignments for your user role. You will need to log out of the user interface to obtain a new session with the new policies.

![](<../.gitbook/assets/image (435) (1) (1).png>)

## Perform Installation Qualification

An easy way to get patients into the SanteMPI instance is to run the [fhir-interface-validation](installation-1/santedb-server/installation-qualification/fhir-interface-validation/ "mention"). These tests will ensure that the MPI is operating correctly (using the default options) and in the process, will create a few test patients.

### Open the SOAP UI Project

In the pre-requisites, a link was provided to the SanteMPI Installation Qualification SOAP-UI project. You can launch SOAP UI on your system and import this project.

![](<../.gitbook/assets/image (432) (1).png>)

This will expose a new project in your SOAP UI project with the SanteMPI endpoints (restricted from the Swagger documentation) shown and a test case called `Installation Qualification`

``![](<../.gitbook/assets/image (430) (1) (1).png>)``

### Start FHIR Mock Service

The installation qualification tool uses PMIR notifications and subscriptions, it is a good idea to start the FHIR Mock service so that your docker container has an endpoint to send these messages to.

![](<../.gitbook/assets/image (444).png>)

### Run Installation Qualification Tests

Double clicking on the `Installation Qualification` test suite will open the test steps for the SanteMPI installation qualification. There are 10 tests (all of which are documented in detail on the [mpi-cr-test-cases-for-fhir](installation-1/santedb-server/installation-qualification/fhir-interface-validation/mpi-cr-test-cases-for-fhir/ "mention")page).

![](<../.gitbook/assets/image (425) (1) (1).png>)

If all tests return green status, it indicates that your copy of SanteMPI is operating as expected for baseline FHIR functions.

## Validate the User Interface

After the qualification tooling has been executed, you can now use the SanteMPI Dashboard to navigate the recent patients that were created in the installation qualification tool.

![](<../.gitbook/assets/image (436) (1) (1).png>)
