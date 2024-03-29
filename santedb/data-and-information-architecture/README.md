# Data & Information Architecture

Architecturally, SanteDB's data architecture is based around the RIM. SanteDB has a conceptual information model which is implemented in 3 different ways:

* Message Models - The representation of the SanteDB Conceptual Information Model  as JSON or XML objects which appear on the wire or when using functions from third party technologies like JavaScript. Message models in SanteDB include:
  * RIM-based XML model (1:1 with conceptual model)
  * RIM-based JSON model (1:1 with conceptual model)
  * JSON based View-Model (conceptual model with expanded properties to prevent round-trips to the server)
* Business Object Model - The BOM in SanteDB is a series of .NET classes which are implementations of the conceptual information model used by all C# plugins
* Physical Model - The representation of SanteDB's conceptual data model in a variety of RDMS systems including Firebird, Postgres, and SQLite.&#x20;

By realizing the SanteDB conceptual model as these three layers, we observe the following benefits:

* New physical persistence layers can be added without impacting the XML or JSON objects.
* Message formats can be adapted to best suit a message format's strengths without introducing kludge  from the persistence / RDBMS layer.
* Tracking fields used at the physical layer don't pollute the business object model or message models
* We can easily swap each layer independent of one another (add features, remove features, etc.)

## Data Lifecycle

SanteDB iCDR and dCDR never store or or directly with external messaging formats inside of the core components. All communications are transformed between components and their destined system software.&#x20;

Take, for example, a client which is querying the SanteDB iCDR using HL7 FHIR (the pattern is identical regardless of message format).

![](<../../.gitbook/assets/image (180).png>)

In this example, the objects are passed as.

<table data-header-hidden><thead><tr><th width="150">Component</th><th width="150">Input</th><th width="150">Output</th><th>Description</th></tr></thead><tbody><tr><td>Component</td><td>Input</td><td>Output</td><td>Description</td></tr><tr><td>FHIR Service</td><td>FHIR</td><td>BOM</td><td><ul><li>Convers the incoming FHIR message or query to RIM</li><li>Converts and resulting response from RIM BOM back to FHIR</li><li>Performs necessary actions for privacy enforcement, auditing, etc.</li></ul></td></tr><tr><td>Local Repository</td><td>BOM</td><td>BOM</td><td><ul><li>Checks configuration/context for applicable storage provider.</li><li>Calls triggers for business rules and connected services</li></ul></td></tr><tr><td>Master Data Manager</td><td>BOM</td><td>BOM</td><td><ul><li>Locates local copy of object for subsequent calls</li><li>Isolates the data fields which the caller is permitted to update.</li><li>Calls the matching service to detect candidate MASTER records which the record may belong.</li><li>Re-writes the object on the persistence pipeline</li></ul></td></tr><tr><td>Matching Service</td><td>BOM</td><td>BOM</td><td><ul><li>Uses the matcher configuration to establish matches.</li><li>Queries / Blocks against the underlying, configured persistence service.</li></ul></td></tr><tr><td>ADO Persistence</td><td>BOM</td><td>Physical</td><td><ul><li>Translate the business object model into the physical model objects.</li><li>Interacts with the underlying storage technology to reliably store, and retrieve data.</li><li>Transaction control (appropriate rollback/commit infrastructure)</li><li>Performs final data layer check (uniqueness, semantic meaning, etc.)</li></ul></td></tr><tr><td>PostgreSQL</td><td>Physical</td><td>SQL</td><td><ul><li>Translates the physical object model in SQL INSERT/UPDATE/SELECT statements</li><li>Maps query expression trees into SQL</li></ul></td></tr></tbody></table>
