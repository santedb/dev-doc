# Concept Sets

{% hint style="info" %}
This page documents a feature in SanteDB 3.0
{% endhint %}

## Introduction

In SanteDB's concept dictionary, a concept set is a collection of concepts which are used for a particular purpose. Concept sets are used for:

* Data Validation - Whether a particular value belongs on a particular data field or relationship
* Drop Downs - In the user interface to drive selections of concepts
* Grouping of related concepts for export/import

Concepts are administered through the **Concept Set** administration page. Concept sets existing in one of three ways:

* As an explicit list of concepts which are members of the set
* As a composition of other concepts sets via "include" or "exclude"
* As a mix of direct inclusions and compositions

## Concept Set

When an administrator visits the **Concept Sets** page in SanteDB, they are presented with a list of concept sets which are registered with their SanteDB instance.

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Administrators may use this page to:

* **Create** a new concept set
* **Delete** an existing concept set
* **View** details of a concept set
* **Search** concept sets

## Creating a Concept Set

Administrators can create a concept set by selecting the **Create** option. This will display a form of minimal properties for establishing a new concept set.

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The fields are as follows:

<table><thead><tr><th width="164">Field</th><th>Description</th><th>Example</th></tr></thead><tbody><tr><td>Name</td><td>Human readable name for the concept set</td><td><code>Species of non-human Patients</code></td></tr><tr><td>Mnemonic</td><td>A unique mnemonic for the concept set. This is what is used in the user interface and database triggers to reference the concept set by a non-changing name.</td><td><code>NonHumanSpeciesConcepts</code></td></tr><tr><td>OID</td><td>A unique object identifier in dotted form which is used to expose the concept set to other systems. This value must be globally unique.</td><td><code>2.25.302938201056853924218</code></td></tr><tr><td>URL</td><td>The URL of the concept set which is used when the concept set is exposed on FHIR interfaces.</td><td><code>urn:myproject:conceptset</code></td></tr></tbody></table>

## Managing Concept Sets

Viewing a concept set will allow administrators see members of the set and modify the core properties.

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Administrators can **export** the concept into any formats (XLSX, CSV, HTML) for consumption in third party systems. The concept set can also be **download** into a dataset format file for import into another SanteDB instance.

Concept properties can be eited using the concept set properties grid edit option.

### Adding Concepts to Set

Concepts can be added to the concept set using the **Add** option in the **Concept Set Expansion** panel. The interface will show a modal allowing the administrator to add an existing concept to the set or define a new concept.

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

Concepts may be added one at a time, or multiples using the expanded add button action.

<figure><img src="../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Once done adding, the concept set is displayed with the concept and the owning set.

<figure><img src="../../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

### Composing Concept Sets

A concept set can also be composed from other concept sets. Concept set composition is performed using the **Compose** option.

<figure><img src="../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Composition of a concept set is either:

* **Include:** All concepts in the specified concept set are considered members of the concept set in which they're composed
* **Exclude**: All concepts in the specified concept set are forbidden for use in the current concept set.

The example above the example concept set will include all concepts in the **Act Status** set with the exclusion of **Concept Status**. When saving, the concept set expansion window is updated.

<figure><img src="../../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

Included concepts from other sets will have their **Member of Set** column populated with the set from which the concept is drawn and cannot be manually removed from the set. Additionally the **Composition** field will be updated to include all registered concept set compositions.

### Uploading Concept Sets

For bulk uploads, administrators may create a concept of many concepts in a CSV sheet and may upload using the provided template:

<figure><img src="../../../../.gitbook/assets/image (539).png" alt=""><figcaption></figcaption></figure>
