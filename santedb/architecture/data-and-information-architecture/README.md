# Data & Information Architecture

Architecturally, SanteDB's data architecture is based around the RIM. SanteDB has a conceptual information model which is implemented in 3 different ways:

* Message Models - The representation of the SanteDB Conceptual Information Model  as JSON or XML objects which appear on the wire or when using functions from third party technologies like JavaScript. Message models in SanteDB include:
  * RIM-based XML model \(1:1 with conceptual model\)
  * RIM-based JSON model \(1:1 with conceptual model\)
  * JSON based View-Model \(conceptual model with expanded properties to prevent round-trips to the server\)
* Business Object Model - The BOM in SanteDB is a series of .NET classes which are implementations of the conceptual information model used by all C\# plugins
* Physical Model - The representation of SanteDB's conceptual data model in a variety of RDMS systems including Firebird, Postgres, and SQLite. 

By realizing the SanteDB conceptual model as these three layers, we observe the following benefits:

* New physical persistence layers can be added without impacting the XML or JSON objects.
* Message formats can be adapted to best suit a message format's strengths without introducing kludge  from the persistence / RDBMS layer.
* Tracking fields used at the physical layer don't pollute the business object model or message models
* We can easily swap each layer independent of one another \(add features, remove features, etc.\)



