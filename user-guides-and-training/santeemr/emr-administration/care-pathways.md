# Care Pathways

{% hint style="info" %}
This page documents a new feature in SanteDB 3.0
{% endhint %}

The SanteEMR plugin allows for the specification of care pathways in SanteDB. A care pathway is a logical grouping of CDSS rules which implement a particular, logical set of clinical protocols to care for a particular condition. Example of how this could be used are:

* Enrolling all children under 60 months in a healthy baby care pathway (vaccinations, weights, growth monitoring, etc.)
* Enrolling all women with a confirmed, active pregnancy status into an ANC care pathways (vaccinations, routine monitoring, etc.)

Care pathways are administered in the `SanteEMR / Care Paths` screen on the administrative user interface. When visiting the care pathway page, adminsitrators are presented with a list of all registered care pathways

<figure><img src="../../../.gitbook/assets/image (540).png" alt=""><figcaption></figcaption></figure>

## Creating/Editing a Care Pathway

A care pathway may be created and edited using the `Create` or `Edit` button on the pathway.&#x20;

<figure><img src="../../../.gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure>

A care pathway is defined with the following properties.

| Field                | Description                                                                                                                                                                                                                                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mnemonic             | The unique name for the care pathway, for example `org.myproject.pathway`                                                                                                                                                                                                                                        |
| Description          | A short human readable name for the care pathway                                                                                                                                                                                                                                                                 |
| Enrollment           | Specifies how patients are enrolled into the care pathway. When `automatic` is selected, and patient registered or updated to match the eligibility criteria - a new care plan with the care pathway will be created. When `manual` is selected, clinicians must manually enroll patients into the care pathway. |
| Eligibility Criteria | Identifies the criteria which a patient must possess to be enrolled into the care pathway.                                                                                                                                                                                                                       |
| Encounter Template   | Indicates the type of encounter that is to be used when new visits in this care pathway are computed.                                                                                                                                                                                                            |

## Adding CDSS to a Care Pathway

CDSS protocols are loosely linked to their care pathway. To add a new rule or protocol to the care pathway, an administrator must first create or change the relevant CDSS library (see: [edit-cdss-library.md](../../../operations/cdr-administration/santedb-administration-panel/cdr-administration/decision-support-library/edit-cdss-library.md "mention")) and place the care pathway into the scope of the protocol. For example, if the care pathway mnemonic is `org.example.anc` any protocols which apply to this care pathway should be tagged as:

```
define protocol "ANC Tetanus / Diptheria Vaccination" 
    having scope <org.example.anc>
```

This indicates that the protocol is to be included and executed whenever a patient is enrolled or appears for an ANC visit.

