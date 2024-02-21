# View CDSS Library

{% hint style="info" %}
This page documents features of a user interface which heavily relies on understanding the [Clinical Decision Support System ](../../../../../developers/extending-santesuite/extending-santedb/applets/cdss-protocols.md)in SanteDB. Readers should be familiar with these concepts prior to reading this page.
{% endhint %}

The View CDSS library option allows administrators to see the CDSS library definition in a format whihc is user friendly, and represents how the SanteDB server environment "sees" the CDSS library. This screen is useful for users who:

* Aren't writing CDSS definitions, but need to manage them via files provided to them from developers
* Are writing CDSS definitions and need to reference the contents of another library in a user friendly manner

<figure><img src="../../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The view screen provides a series of tabs, and panels which are used for gathering information about the status of the CDSS library.

## Library Properties

The library properties panel is used to display core attributes of the CDSS library, including metadata related to documentation, identification, authorship and maintenance.

<figure><img src="../../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

## Version History

SanteDB's CDSS engine will keep previous versions of the CDSS library. This is important as care plans and actions taken based on previous versions of the CDSS library may be important for understanding the context in which a care decision was made.

<figure><img src="../../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
A previous version of a CDSS library can be restored by downloading the definition for the desired version and uploading it.
{% endhint %}

## Logic Blocks

The logic tab is used to render the CDSS decision logic which the library contains. This tab will contain representations of any **fact, protocol, rule, model** or other logic elements defined. These definitions can be expanded by the administrator by clicking on the title of the definition to be expanded.

<figure><img src="../../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## Reference Data

The **Reference Data** tab is used to downloading a copy of the reference data sets defined by the CDSS library. These reference data sets contain data such as reference values, ranges, pre-computed z-scores, etc. which are useful for making interpretations, or modifications to an object.

<figure><img src="../../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## Upload New Version

Administrators can use the **Upload** option in the header of the view CDSS library page to upload a new CDSS definition (from another server, from a developer, etc.). The administrator should select a new CDSS source file or an XML file downloaded from another SanteDB server, and press **Upload** when complete.

<figure><img src="../../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
