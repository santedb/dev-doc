# Extending & Customizing SanteDB

SanteDB provides a variety of mechanisms for extension and customizing the manner in which it operates. The most common ways to modify the behavior of SanteDB are:

* Configuration
* Applets
* .NET Plugins
* API Access
* End-User Extensions

## Configuration

SanteDB supports a very robust configuration system, and many of the built-in plugins and services may support the use-case and workflow you're looking to implement. Check the service's configuration documentation for more information on how SanteDB's services can be modified simply by editing a configuration file.

The tools required for customizing SanteDB products by configuration are:

* Virtualization Software
* An XML-Aware Text Editor (Visual Studio Code, Notepad++, etc.)
* SanteDB administration console and ConfigTool

The [configuration-tool](../../operations/server-administration/configuration-tool/ "mention") is the primary method of customizing SanteDB.

## Applets

[applets](extending-santedb/applets/ "mention") are written in JavaScript, and HTML. Applets allow developers who are interested in customizing the user interface of SanteDB with custom screens, widgets, etc. Applets also provide an opportunity to easily apply branding, translation, and behavior modification through further customization provided by the built-in plugin infrastructure.

### Capabilities

When extending SanteDB using applets, the following extension capabilities are available:

* Adding new screens and controllers to the user interface (such as the administrative panel, EMR user interface, etc.)
* Adding new business rules to the iCDR or dCDR
* Adding new BI reports, indicators, shared queries, parameters, etc.
* Adding new Clinical Decision Support rules&#x20;
* Customized data import formats
* Adding new widgets (tabs and panels) to existing screens in the UI

### Toolchain

Tools which can assist in the development of applets are:

* Community Code Signing Certificate ( [santedb-software-publishers](../santedb-software-publishers/ "mention") )&#x20;
* Microsoft Visual Studio Code
  * RedHat XML Plugin ([https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml))
* SanteDB Software Development Kit ( [installing-the-dcdr-sdk.md](../../installation/installation-1/deployment/installing-software/disconnected-gateway/installing-the-dcdr-sdk.md "mention") )
* A SanteDB iCDR server against which you can test your extensions

## .NET Plugins

[server-plugins](extending-santedb/server-plugins/ "mention") are best for those looking to do heavier customization such as adding support for a new database system, API call, authentication scheme, merge/data management scheme, etc. SanteDB's robust .NET plugin infrastructure may provide the best path.&#x20;

### Capabilities

The capabilities exposed in the .NET plugin customization route are pretty boundless, but typically .NET plugins are used for:

* Extending the FHIR behaviors (adding operations, message types, extensions or resources)
* Extending the HDSI or AMI APIs to support new resources, operations, and child behaviors
* Integrating with new solutions (new Message Queue servers, third party data targets)
* Advanced / higher performance business rules (such as assigning stock, automatic creation of data from third party systems on triggers)
* Adding database schema elements or changing persistence implementations (supporting new data storage, adding new database technologies, etc.)

### Toolchain

The toolchain for development of plugins in .NET are:

* Community Code Signing Certificate ( [santedb-software-publishers](../santedb-software-publishers/ "mention") ) or a valid Authenticode Code Signing Certificate
* Microsoft Visual Studio Code
* Microsoft Visual Studio Community Edition 2022 (Professional or Enterprise also work)
* Inno Setup Compiler 6.0 or higher
* Microsoft .NET Framework 4.8 or higher
* Fiddler4 (or equivalent debugging proxy)

## API Access

Nearly 100% of SanteDB's services are exposed as REST-based APIs, you can extend SanteDB by writing custom software and calling those APIs. This process involves using your own development stack and tools of your choice and consuming one of the many [service-apis](extending-santedb/service-apis/ "mention")available.

### Capabilities

Typically those writing applications against the SanteDB APIs do so to:

* Integrate SanteDB with another application that is already in use using APIs
* Leverage SanteDB services to leverage one piece of the platform (i.e. calling CDSS as a service)
* Extracting data from SanteDB and placing it into another system

## End-User Extension

SanteDB 3.0 includes many screens in the adminsitration panel which allow adminsitrators to customize the deployment of SanteDB from within SanteDB. These tools also allow for export of configurations and import into other SanteDB solutions.

### Capabilities

The capabilities which are available when using the SanteDB administration user interfaces to customize the platform are:

* New CDSS rules and libraries
* New Data Quality rules and libraries
* New Clinical Data Templates and libraries
* New Encounter Types & Care Pathways
* New Reference Terminologies, Concept Sets, and concepts
* Customized place, facility, material lists

## Topics

{% content-ref url="extending-santedb/applets/getting-started.md" %}
[getting-started.md](extending-santedb/applets/getting-started.md)
{% endcontent-ref %}

{% content-ref url="extending-santedb/applets/" %}
[applets](extending-santedb/applets/)
{% endcontent-ref %}

{% content-ref url="extending-santedb/server-plugins/" %}
[server-plugins](extending-santedb/server-plugins/)
{% endcontent-ref %}

{% content-ref url="extending-santedb/service-apis/" %}
[service-apis](extending-santedb/service-apis/)
{% endcontent-ref %}

{% content-ref url="../santedb-software-publishers/" %}
[santedb-software-publishers](../santedb-software-publishers/)
{% endcontent-ref %}
