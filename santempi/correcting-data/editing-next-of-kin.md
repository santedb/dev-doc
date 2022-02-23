# Related Persons Panel

{% hint style="info" %}
Related persons are linked entities to the patient. When you edit the information for a family member within the patient view, you're actually editing information on another record. This may result in a shared update if the target family member is strongly linked between entities.
{% endhint %}

A patient's next of kin is displayed in the **Related Persons** panel and can be edited by clicking the **pencil** icon.

![](<../../.gitbook/assets/image (417).png>)

## Editing Existing Family Members

Clicking the edit button on the related persons panel will allow the administrator to change the demographic information about the related person.&#x20;

{% hint style="info" %}
In SanteDB (and SanteMPI) the family members of patients may be a Person record (a non-patient person) or may be a patient record. This distinction will depend on the nature in which the related person is registered. For example, if the registration occurs via an HL7v2 NK1 segment and the identifier points to an existing patient, then the MPI constructs a Patient<>Patient link, however if the NK1 links to a new record then the relationship is created as Patient<>Person link.
{% endhint %}

![](<../../.gitbook/assets/image (452).png>)

### Editing Patient Family Members

In the case where a related person is another patient, the act of editing the information on the related persons tab will result in a new MASTER record being created for the patient which is the family member. This is indicated on the **Advanced** relationship graph as a MDM rewrite.

For example, the record for **Baby Abels** has a mother **Sarah Abels** both of which are Patient types (this record is registered in[test-ohie-cr-05-fhir.md](../../installation/installation-1/deployment/software-deployment/santedb-server/installation-qualification/fhir-interface-validation/mpi-cr-test-cases-for-fhir/test-ohie-cr-05-fhir.md "mention")).\


![](<../../.gitbook/assets/image (436).png>)

When editing the data in the relationship panel, the information appears as illustrated below:

![](<../../.gitbook/assets/image (455) (1).png>)

The editing of information on this panel (in this particular case) is redirected as an edit of the Record of Truth which is attached to Sarah Abels.

## Adding Related Persons

Related persons can be added to the patient's profile using the **New** tab. Before adding a new relationship, the user must select the nature of the relationship and complete the minimum dataset for the related person (depending on implementation, usually this is only name).

![](<../../.gitbook/assets/image (449) (1).png>)

## Related Topics

{% content-ref url="../../santedb/data-and-information-architecture/conceptual-data-model/entities/entity-relationships.md" %}
[entity-relationships.md](../../santedb/data-and-information-architecture/conceptual-data-model/entities/entity-relationships.md)
{% endcontent-ref %}
