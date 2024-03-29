---
description: The structure of a SanteDB applet
---

# Applet Structure

There are very few hard requirements regarding the structure of your applet. Your applet root directory is treated as the root of a web-server, so you can use whichever client libraries and tools you like to develop your applet. It really is possible to write a disconnected clinical application using your favorite HTML & JavaScript tools.

There are, however, some benefits to following the SanteDB user interface elements. The applets which are readily available for use are:

| Applet              | Dependencies                                       | Description                                                                                    |
| ------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| org.santedb.core    | None                                               | Core API library. Provides the SanteDB JavaScript API.                                         |
| org.santedb.uicore  | org.santedb.core                                   | AngularJS based core UI components (provides controls listed on AngularJS page)                |
| org.santedb.bicore  | org.santedb.uicore                                 | BI core functions for rendering reports generated by the Business Intelligence Services layer. |
| org.santedb.config  | org.santedb.uicore                                 | Core configuration screens for the key functions of the SanteDB client.                        |
| org.santedb.admin   | <p>org.santedb.uicore</p><p>org.santedb.bicore</p> | SanteDB administrative panel                                                                   |
| org.santedb.i18n.en | None                                               | Registers the English Language assets                                                          |
| org.santedb.i18n.fr | None                                               | Registers the French Language assets                                                           |
| org.santedb.i18n.es | None                                               | Registers the Spanish Language assets                                                          |
| org.santedb.i18n.sw | None                                               | Registers the Swahili Language asset                                                           |

### Manifest File

The only required file for an applet is the Manifest.xml file. This file is used by the packager to generate a bundle manifest. The manifest file contains:

* Metadata information such as applet author, version, dependencies, etc.
* Translations / String definitions for any languages your applet displays
* Menu registrations for extending the UI menus
* Error asset registrations which are rendered in-lieu of stock error pages
* View model definitions for instructing the API which attributes should be "deep loaded"
* Locale definitions which inject javascript into the core header for the applet pages based on the user's current locale.
* Data setup instructions which are used to insert special data elements which are (not synchronized on the server).
  * Note: This is a legacy function, you should instead use dataset files in the Data/ directory
* Configuration settings which your applet or other plugins use to customize the core engine features.
* Template registrations which indicate templates you can use for constructing / pre-populating objects.

### Key Structures

Certain plugins built into SanteDB will look for particular files to be placed in particular paths.&#x20;

| Path                                             | Plugin                    | Description                                                                                                                                                                                                         |
| ------------------------------------------------ | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .ref/                                            | Compiler                  | Any folders beginning with a . are ignored. The .ref directory is typically used to store references for code-completion.                                                                                           |
| [bi/](business-intelligence-bi-assets/)          | Business Intelligence     | The bi definitions folder is scanned by the Business Intelligence service on startup, and BI assets are registered for use (for reporting, creating FHIR MeasureReports, executing ad-hoc data queries, etc.)       |
| [dataset/](distributing-data.md)                 | Dataset Installer         | The data folder is scanned on startup by the dataset installer and any dataset files present in this folder are installed to the server's database.                                                                 |
| model/                                           | View Model                | The view models folder contains view model definitions which are used to deep-load data.                                                                                                                            |
| [protocols/](cdss-protocols.md)                  | Clinical Decision Support | The protocols folder is scanned by the clinical decision support engine and provides the master list of protocols to be executed by the CDSS engine.                                                                |
| [rules/](business-rules.md)                      | Business Rules Engine     | The rules folder is scanned by the JavaScript BRE engine. This engine is a server-side (and client side) ECMA5 environment. This ensures that business rules are executed in the same way on the server and client. |
| match/                                           | Matching Engine           | The matching engine configuration directory is used to configure the SanteDB matching engine.                                                                                                                       |
| [alien/](../../../applets/external-data-maps.md) | Alien Data Format Maps    | Stores data import configurations which can be used to load and convert external data formats into SanteDB format.                                                                                                  |
| notifications/                                   | Notification templates    | Stores custom notifications for e-mails and text messages.                                                                                                                                                          |
