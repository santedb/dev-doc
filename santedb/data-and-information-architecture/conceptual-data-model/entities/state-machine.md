# State Machine

Entities also support a basic series of states which identify the current status of the entity in the SanteDB data model. Figure 7 illustrates the states of an entity and the valid transitions.

![Figure 7 - Entity State Diagram](<../../../../.gitbook/assets/image (329).png>)

The states of the entity are:

* **New :** The entity instance was just created, and no processing, storage, or business rules have been executed.
* **Active :** The entity has been persisted, any necessary review and/or processing has occurred, and the entity record is active.
* **Nullified :** Indicates that the entity was created in error, the entity never existed.
* **Obsolete :** Indicates that the entity did exist, however it no longer is active.
