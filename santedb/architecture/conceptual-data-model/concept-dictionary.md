# Concept Dictionary

One of the central design principles in SanteDB is that of customizable code and valuesets to be used within the SanteDB system. The concept subset of tables within the data model are used to store the master dictionary of concepts used within the SanteDB system.

There are four major facets of the concept system in SanteDB:

* **Concept Classes:** A concept class is a classification of what a concept represents. Concept classes are used for validation and organizing the concept dictionary. Examples of a concept class could be UnitOfMeasure for concept which are units of measure.
* **Concepts:** A concept is a central idea of an object or attribute of an object within the SanteDB database. A concept is, technically speaking, an abstract object which describes a real world thing. For example, the concept of an Arm, or the concept of OPV.
* **Reference Terms:** A reference term is a wire level representation of a concept. A reference term represents a manner in which a concept can be represented to another system. For example, the concept of OPV in the HL7 CVX reference term set is ‘01’.
* **Concept Sets:** A concept set represents a collection of concept that may be used for a particular purpose. Concept sets are used to restrict the complete set of concepts within the SanteDB database to those applicable in a particular scope. For example, an entity classification concept must be selected from the EntityClass concept set.



