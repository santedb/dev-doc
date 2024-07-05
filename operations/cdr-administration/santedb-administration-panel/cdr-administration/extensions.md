# Extensions

{% hint style="info" %}
This page documents a feature in SanteDB 3.0
{% endhint %}

Extensions are used to allow SanteDB to store additional, unstructured data which exists outside of the normal CDR persistence model. Extensions are used in SanteDB:

* To store additional information which is attached to a resource (see: [extended-data.md](../../../../santedb/data-and-information-architecture/conceptual-data-model/extended-data.md "mention"))
* To accept (verbatim) data which is provided via a FHIR extension directly into the database without writing an extension handler (see: [#extension-handlers](../../../../developers/santedb-software-publishers/extending-fhir-interfaces.md#extension-handlers "mention"))

Extensions, unlike tags (which are simple key/value pair data) must be registered with a type. To use the administration console to manage extensions administrators should access the **CDR Administration > Extensions** page.

{% hint style="warning" %}
Deleting or changing the URI of an extension which is in use may cause problems at the interoperability layers of SanteDB (FHIR, HDSI, etc.)
{% endhint %}

## Extension Registry

The types of extensions which are registered in SanteDB lists summary information about all of the accepted extensions in your SanteDB instance.

<figure><img src="../../../../.gitbook/assets/image (537).png" alt=""><figcaption></figcaption></figure>

The extension registry allows administrators to:

* View and edit the extension detail for each registered type of extension
* Delete or un-register the extension type
* Create a new extension type
* Export the list of extension registrations to a dataset (to be imported into another SanteDB instance)

## Creating/Editing an Extension Type

Creating an extension type is relatively straightforward, administrators should use the **Create** option from the registry to create a new extension type. The administrator is presented with a blank editing screen.

<figure><img src="../../../../.gitbook/assets/image (538).png" alt=""><figcaption></figcaption></figure>

The fields for the extension type are listed below.

<table><thead><tr><th width="209">Field</th><th>Description</th></tr></thead><tbody><tr><td>Name/Description</td><td>A human friendly name for the extension type (how it should appear in user interfaces)</td></tr><tr><td>URI</td><td>A unique (within the SanteDB instance) url or urn which is used to identify the extension. If using this extension type to store FHIR data, then this should match the FHIR URI</td></tr><tr><td>Type Handler</td><td>The type handler instructs SanteDB how the data in the extension should be serialized and indexed, the options are documented below.</td></tr><tr><td>Applies To</td><td>If the extension's use is restricted to certain resource types, enumerate them here.</td></tr></tbody></table>

### Extension Type Handlers

| Handler    | Serialized As                                                                                                                                        | Examples                                               |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| Binary     | Binary data (`bytea or blob`) and base64 on messages                                                                                                 | Pictures, Biometric Data, Streams, etc.                |
| Boolean    | One byte value in database and true/false string on messages                                                                                         | Indicators, Yes/No data                                |
| Date       | 64-bit integer in database and ISO date string on messages                                                                                           | Dates, Date/Time data.                                 |
| Decimal    | 128-bit decimal number in database and decimal number in messages.                                                                                   | Account Balances, Weights, Numeric data.               |
| Dictionary | A serizlied JSON object                                                                                                                              | Structured data                                        |
| Reference  | A reference to either a `Concept`, `Entity` or `Act` in the format `SPEC^UUID` where SPEC identifies the type and UUID identifies the target object. | Coded extension data, reference data (to places, etc.) |
| String     | Alphanumeric string data                                                                                                                             | Freeform text                                          |
| UUID       | 128-bit number in database, serialized UUID in the format `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx`                                                       | Identifiers, pointers to other data.                   |

