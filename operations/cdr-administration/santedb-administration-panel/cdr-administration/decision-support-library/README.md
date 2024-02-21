# Decision Support Library

All copies of SanteDB's iCDR and dCDR can execute clinical decision support rules. SanteEMR and its derivative (SanteIMS) enhances the administrative process for management of decision support rules by allowing administrators to author decision support rules from the user interface.&#x20;

These rules are then downloaded for offline use in the dCDRs and the SanteEMR encounter screens to propose care plans.

When accessing the SanteDB CDSS Library screen, the user will be presented with a summation of the decision support libraries available in the SanteEMR instance.

<figure><img src="../../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

The information provided on this screen is:

* Name: Identifies the human-friendly name for the library, its unique dotted identifier (example: `org.example`) and its universal external OID (such as IANA PEN, etc.).
* Info Version: Shows the informational version (or declared version) of the library.&#x20;
* Status: Identifies the current status of the CDSS library:
  * Active: The library is in use. Whenever the CDSS engine is asked to create care plans, this contents of this library will be considered.
  * Trial Use: The library is only being used for a select number of patients (based on whether the CDSS is called with `isTrial` )
  * Retired: The library will be used to refresh existing care plans upon which they were originally based, however will not be used for new plans.
  * Don't Use: The library will never be used and explicit calls to it will result in a CDSS error.

Executable library definitions can be downloaded directly from the index page using the **Download** option. This file can be uploaded to other SanteDB instances to register the rule on another server. This is useful when moving rules from a staging environment to a production environment.

## Creating CDSS Library

A CDSS library can be created using the **Create** button on the CDSS library screen. When creating a library two options are presented:

<figure><img src="../../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* **Upload CDSS Library File:** Allows an administrator to select a CDSS definition file either in executable XML format or in the source CDSS format.
* **Manually Create CDSS Library:** Allows for the entry of CDSS metadata fields to register a new, empty CDSS library.

When manually creating a CDSS library, the metadata inputs will be used to construct a scaffolded CDSS library in the SanteDB server instance.

<figure><img src="../../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

* **Name:** The human friendly name for the CDSS library. In the definition file this becomes the contents of `define library NAME OF LIBRARY` and should be unique in the scope of the SanteDB server.
* **Identifier:** The unique "computer" identifier for the CDSS library. This should be unique for all of SanteDB instances and should be a dotted identifier. Typically the naming convention of `mycountry.myproject.mysubproject.library` should be used, for example, in the Canadian Province of Ontario , a library for calculating HPV dosing may have an identifier of `ca.on.epi.vaccine.hpv`
* **OID:** If using an IANA PEN enter the dotted OID identifier for this CDSS library here, if not using IANA PENs or any other OID based identification you can enter a random OID here such as `2.25.XXXXX`
* **Stated Version:** This is the version of the CDSS library that will follow it when it moves between SanteDB servers, and should be an informative version id in a semantic versioning format.
* **Author/Description:** Information about the CDSS library that will be moved with the definition file between servers.

After creating a new CDSS library you will be redirected to either the View CDSS LIbrary page (in the case of uploading) or the Edit CDSS LIbrary page (when defining a new CDSS library).
