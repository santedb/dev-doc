# Virtual Appliances

SanteDB provides a number of virtual appliances to assist in the rapid deployment of service environments. 

## Virtual Appliance Types

### Headless Server Environment

You should use the headless server environment virtual appliance when deploying an instance of SanteDB \(and related solutions\) for light production duty, or development. These virtual appliances include:

* Ubuntu Server 20.04
* Mono Framework 6.2
* PostgreSQL 10
* SanteDB iCDR Server
* SanteDB Administrative Portal

### Developer Environment

You should use the developer environment virtual appliances when you need to rapidly onboard developers. These virtual appliances contain not only the SanteDB iCDR and dCDR environments, but the SanteDB SDK tooling, and related software including:

* Ubuntu 20.04
* XFCE4 Desktop Environment
* MonoDevelop 
* PostgreSQL 10
* Visual Studio Code 
* DBeaver Community Edition
* SanteDB iCDR Server
* SanteDB dCDR Server
* SanteDB SDK

## Configuring the Virtual Appliances

### **Shell Access**

**User:** sante  
**Password:** SanteDB123  
After deploying and setting up the OVA, you should either:

* Setup a host entry or DNS entry for **santempi.local** which points to the IP address of the appliance in your environment, or
* Edit the /etc/nginx/sites-available/santedb file and edit the server\_name to use your own DNS entries

The service requires that port 80 and 8080 be opened to allow for administrative and API access from other hosts respectively.

### Initial Settings & Directories

| Setting | Value |
| :--- | :--- |
| SanteDB iCDR Location | /opt/santedb/server |
| SanteDB dCDR Location | /opt/santedb/dcdr-www |
| iCDR API Port | http://127.0.0.1:18080 |
| dCDR API Port | http://127.0.0.1:9200 |
| API User | Administrator |
| API Password | Mohawk123 |

