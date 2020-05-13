# Entities

An entity within the SanteDB data model is used to represent a person, place, or thing. Entities represent the who, which and where aspects of an action. Entities are further classified into several sub classes illustrated in Figure 1.

![Figure 1 - Entity Classes](../../../../.gitbook/assets/image%20%2888%29.png)

### Class Codes

Entities are further classified by their class code and determiner code. The determiner code of an entity is responsible from differentiating a type of an entity \(i.e. antigen, dose number, material type, etc.\) and an instance or series of instances of an entity \(an actual vial of vaccine, a box of syringes, etc.\). Most entities within the SanteDB system are expected to be stored as instances of entities, classes of entities will primarily be restricted to materials whereby a class of antigens \(OPV for example\) will have both instances \(vials of OPV\) and sub-classes of representing dose numbers \(OPV0 – OPV3\). Provides a summary of the entity classes and how they are classified in the data model.

| **Entity Class** | **Class Code** | **Description** |
| :--- | :--- | :--- |
| Entity | ENT | An entity is the base class used to represent a person/place/thing in the SanteDB data model. |
| Material | MAT | A material represents a physical thing to which participates in the delivery of care. For example: a syringe, a box of vaccine, etc. |
| Manufactured Material | MMAT | A manufactured material represents a material which is manufactured such as diluent, vaccine, syringes, etc. |
| Place | PLC | A place represents a physical location where health services are provided. |
| Organization | ORG | An organization represents an administrative structure which employs providers, operates clinics, etc. |
| Person | PSN | A person represents a human being. |
| Patient | PAT | Represents a person who receives health services. |
| Provider | PVD | Represents a person who provides health services. |
| User | USR | Represents a person who actively uses the system. |
| Device | DEV | Represents a physical object on which health services data is entered, stored, etc. |
| Application | APP | Represents a piece of software which is used to access, record or update medical data. |

### Determiner Codes

Determiner codes are used to classify whether a tuple in the entity table represents an actual thing or a classification of things. There are three types of determiner classifications for objects listed in .

| **Determiner** | **Description** | **Example** |
| :--- | :--- | :--- |
| Instance | The entry in the database represents a one or more occurrences of an entity. | A patient, a facility, an organization, etc. |
| Kind | The entry represents a classification of entities. | A type of material, a type of organization, a type of device. |
| Quantified Kind | Represents a kind of object which is quantified such as X number of Y. | A dose of vaccine \(5ml, etc.\) |

### Relationships

Figure 2 represents a sample information model of a kit of BCG vaccine. The model illustrates how a single tuples in the SanteDB model are related to one another to represent a kit. The material “BCG Vaccine” is comprised of one dose of “BCG Antigen”, one “Syringe”, and one dose of “BCG Diluent”. A box of “BCG Vaccine” represents 25 single doses of “BCG Vaccine” \(meaning 25 syringes, 25 antigen and 25 diluent\). Finally, from this we can order \(via instantiation or inheriting a kind\) a kit of GSK 5ml BCG vaccine. This derivation will have the same rules applied \(in that this vaccine must have a syringe, antigen, and diluent.

![Figure 2 - Kitting of BCG](../../../../.gitbook/assets/image%20%2837%29.png)

Figure 3 represents a complex scenario of kitting a vaccine and then deriving a specific type of kit. The relationship between the instantiation and the generic concepts of the material would have a type of “Manufactured” meaning the “GSK 5 ml BCG” is a manufactured representation of the generic BCGvaccine.

![Figure 3 - Instantiating BCG Vaccine kit to Manufactured Materials ](../../../../.gitbook/assets/image%20%281%29.png)

The SanteDB model also supports more simplistic representation of a “BCG Vaccine” if kits are not required by the jurisdiction that is implementing SanteDB. Figure 4 illustrates a valid representation of BCG in a jurisdiction where only the antigen is tracked.

![Figure 4 - Representing an instance of a KIND of Entity](../../../../.gitbook/assets/image%20%2835%29.png)

### States

Entities also support a basic series of states which identify the current status of the entity in the SanteDB data model. Figure 7 illustrates the states of an entity and the valid transitions.

![Figure 7 - Entity State Diagram](../../../../.gitbook/assets/image%20%2870%29.png)

The states of the entity are:

* **New :** The entity instance was just created, and no processing, storage, or business rules have been executed.
* **Active :** The entity has been persisted, any necessary review and/or processing has occurred, and the entity record is active.
* **Nullified :** Indicates that the entity was created in error, the entity never existed.
* **Obsolete :** Indicates that the entity did exist, however it no longer is active.

