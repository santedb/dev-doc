# Entity Relationships Panel

The entity relationships panel is a display only panel that illustrates the physical and logical relationships between different entities in the SanteDB database.

The relationships panel is useful when administrators are attempting to understand the underlying data relationships for the current record being displayed.

![](<../../../../.gitbook/assets/image (444) (1).png>)

The current focal object for the diagram (the object which the current page is displaying) is always shown as a green circle. In this case the focal record is **KATHLEEN R SKERSIES** entity.

Entity relationships are illustrated with a directional arrow with the source/holder entity (the entity on the end of the connector with no arrow) links to the target entity (the entity on the end of the connector with an arrow).

Entities can be related in several manners:

| Relationship      | Example                                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Physical          | ![](<../../../../.gitbook/assets/image (427).png>)     | <p>A physical relationship is represented by a solid line with directional arrow indicating the direction of the relationship.<br>Physical relationships between entities indicate that the relationship exists in the database in the <code>ent_rel_tbl</code> and physically links the two records via UUID.</p>                                                                                                                                                                                                                                                                                                                                                                                      |
| Inferred/ Logical | ![](<../../../../.gitbook/assets/image (459).png>)     | A logical relationship is a relationship which can be inferred between two entities from other information. These are most commonly found on MASTER records when a local entity has a relationship, however that relationship has been promoted to the master.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| MDM Rewrite       | ![](<../../../../.gitbook/assets/image (435) (1).png>) | <p>A MDM rewritten relationship is used to show a case where a SOURCE entity is related to another SOURCE entity, however the MDM layer controls both the target and holder entity types. The MDM layer rewrites this relationship for so that the target points to the MASTER of the intended target. <br><br>For example: <code>SOURCE_PATIENT_A</code> is related to <code>SOURCE_PATIENT_B</code> , when viewing <code>MASTER_A</code> the relationship between <code>SOURCE_PATIENT_A</code> and <code>SOURCE_PATIENT_B</code> is shown as <code>SOURCE_PATIENT_A</code> <code>MASTER_B</code> with <code>MASTER_A</code> being related to <code>MASTER_B</code> via an inferred relationship.</p> |

The entities which are being related to one another are shown as boxes with a colour coding and icon which indicates the type of object.

| Entity Type                          | Example                                                | Description                                                                                                                                                   |
| ------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Entity (no special attributes)       | ![](<../../../../.gitbook/assets/image (448).png>)     | Entities which are the target of a relationship and are navigable (normal condition) are shown with a solid border, and a link to the entity being expressed. |
| Record of Truth / Verified           | ![](<../../../../.gitbook/assets/image (456).png>)     | Entities which are validated, sources of truth are shown in gold with a solid border and a link to the data which has been validated.                         |
| Entity (target / no viewer)          | ![](<../../../../.gitbook/assets/image (438) (1).png>) | Entities which are not validated, and do not have a special viewer are shown as a dotted border in pink.                                                      |
| Source / Reverse Relationship Entity | ![](<../../../../.gitbook/assets/image (454).png>)     | Entities which are the source (or which point AT the focal record) are shown with a dotted border.                                                            |

## View Mode

The view mode of the relationship graph allows administrators to switch the representation of the relationships between a simplified view (where inferred relationships are preferred over physical - to simplify the diagram) and an advanced view.

The simple view below indicates that Kaleen R Skersies (focal record) has a SOURCE (pointing at it as a Master Record) has a Record of Truth (pointing outbound) and an inferred relationship as a Citizen to Canada and a Mother to JONES.

![](<../../../../.gitbook/assets/image (460).png>)

Administrators looking at the same entity in advanced mode will be able to determine the true source of inferred relationships as well as any MDM redirects. For example, the advanced view below show.

With advanced view mode enabled, administrators can now see that the Citizen relationship is actually physically linked via the record of truth and the mother relationship has been linked via the SOURCE record.

![](<../../../../.gitbook/assets/image (437).png>)

## Related Topics

{% content-ref url="../../../../santedb/data-and-information-architecture/conceptual-data-model/entities/entity-relationships.md" %}
[entity-relationships.md](../../../../santedb/data-and-information-architecture/conceptual-data-model/entities/entity-relationships.md)
{% endcontent-ref %}
