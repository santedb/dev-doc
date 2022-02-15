# Identifiers Panel

The identifiers panel shows the collected identification numbers collected from source systems in the MPI. This function is what allows the MPI to cross reference identification between different systems.

## Editing Identifiers

Identifiers can be edited within the administrative portal if :

* The portal has direct authority to edit the identifier type or the identifier can be globally assigned.
* The identifier type is scoped in a way that it can be assigned to a ROT
  * For example: If an identifier is scoped to a Master Entity (such as a national health id) then the portal cannot change or assign a new identifier in that domain.

![](<../../.gitbook/assets/image (439).png>)

### Changing Identifiers

{% hint style="info" %}
Changing an identifier is not recommended if the administrative panel was not the original source of the identifier. It is good practice to correct invalid identifiers on the source system.&#x20;

If you're editing an identifier on a master record, then the identifier originally sent by the source system will not be changed, only the Record Of Truth record will carry the new identifier.
{% endhint %}

To change an identifier users should first remove the existing identifier from the list and save the patient record, then re-add the identifier value to the list.

### Adding an Identifier

To add an identifier to the patient's record you can select the identity domain of identifier to be added, and add the identifier to the list.

![](<../../.gitbook/assets/image (56).png>)

### Identifier Generators

SanteMPI provides API hooks to generate random identifiers based on some sort of algorithm. If an identity domain has a generator attached, a generation icon will appear next to the add button which can be used to generate the identifier.

![](<../../.gitbook/assets/image (87).png>)
