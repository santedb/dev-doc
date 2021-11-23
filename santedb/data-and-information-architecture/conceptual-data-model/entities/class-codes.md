# Class Codes

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

