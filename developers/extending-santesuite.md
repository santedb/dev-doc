# Extending SanteSuite



SanteDB provides a variety of mechanisms for extension and customizing the manner in which it operates. The most common ways to modify the behavior of SanteDB are:

* **Configuration: **SanteDB supports a very robust configuration system, and many of the built-in plugins and services may support the use-case and workflow you're looking to implement. Check the service's configuration documentation for more information on how SanteDB's services can be modified simply by editing a configuration file.
* ****[**Applets**](applets/)**: **Applets are written in JavaScript, and HTML. Applets allow developers who are interested in customizing the user interface of SanteDB with custom screens, widgets, etc. Applets also provide an opportunity to easily apply branding, translation, and behavior modification through further customization provided by the built-in plugin infrastructure.
* [.**NET Plugins**](server-plugins/)**: **For those looking to do heavier customization such as adding support for a new database system, API call, authentication scheme, merge/data management scheme, etc. SanteDB's robust .NET plugin infrastructure may provide the best path.&#x20;
* ****[**Business Intelligence Services**](applets/business-intelligence-bi-assets/)**:** If you're just looking to extract data from SanteDB for use with FHIR's Measure Report, the Report Centre, or DHIS2 you can do this by writing BI service components. BI services components interact with the underlying database infrastructure of SanteDB and require only knowledge of SQL and light XML editing.
* ****[**API Access**](service-apis/)**: **Finally, because nearly 100% of SanteDB's services are exposed as REST-based APIs, you can extend SanteDB by writing custom software and calling those APIs.&#x20;
