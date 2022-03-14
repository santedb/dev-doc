# SanteMPI Patient Detail

When opening a patient in a search result, match result, or via direct link, users will be presented with an overall dashboard of the patient.

## Patient Header

Located at the top of the patient detail is the patient header. The header shows summary information about the patent record.

![](<../.gitbook/assets/image (429) (1) (1).png>)

### Record Status

The SanteDB CDR supports assigning a status identifier to a record in the system. These states can be set by initiating a state transition, which map to the [state-machine.md](../santedb/data-and-information-architecture/conceptual-data-model/entities/state-machine.md "mention") in the CDR information model. To change the status of a record users can click on the status indicator and select a transition to be applied.



![](<../.gitbook/assets/image (448) (1) (1).png>)

| State       | Description                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `NEW`       | <p>The record has been submitted from an external system, a user interface, or has been created with no specified state. The <code>NEW</code> state can be used to indicate that a record has not been reviewed, merged/linked, or reconciled. <br>This state is the same (for filtering) as <code>ACTIVE</code> , it indicates the record is "Active" but unreviewed.</p>                                              |
| `ACTIVE`    | The record is active and in use and (depending on the implementation's context) has been reviewed (or was entered by a human on a user interface).                                                                                                                                                                                                                                                                      |
| `INACTIVE`  | The record was active (it was a real record) however it has been indicated as no longer active or accurate. This is the default state in which a `DELETE` request on 2.2.x of SanteDB is placed. Inactive does not indicate why the record is not active, merely that it is inactive. By default, inactive records do not appear in search results and are not considered match candidates (they are logically deleted) |
| `OBSOLETE`  | The record was active (it was a real record) however the information contained in the record is no longer considered accurate and is being kept for historical reference.                                                                                                                                                                                                                                               |
| `NULLIFIED` | The record was never intended to exist (it was created in error). Nullified records are a special case where a record is created in error and anyone viewing the record should consider it a mistaken data entry issue.                                                                                                                                                                                                 |

{% hint style="info" %}
Specific states and state transitions should be defined by the implementing nation to match their workflow. For example, `New` may have a different semantic meanings between jurisdictions
{% endhint %}

### Record Type

When [master-data-storage.md](../santedb/data-storage-patterns/master-data-storage.md "mention") is enabled (as is default in SanteMPI), records can exist in one of three classifications which are indicated by their status bar.&#x20;

#### Local / Source Records

A local or source record indicates that the data being viewed is the SanteDB representation of data submitted directly from a source system.  Source records are read only in the user interface, this is because editing a source record would cause a mis-match of data between SanteDB and the source system which submitted the data (and loss of context). Corrections to local records should be performed on the local system which submitted the data.

![](<../.gitbook/assets/image (427) (1) (1).png>)

#### Master Records

A master record indicates that the data being viewed is collected form a series of local records and is being presented as a logical projection of the data contained in the underlying records.&#x20;

![](<../.gitbook/assets/image (450) (1) (1) (1) (1).png>)

In SanteMPI all LOCAL records must have a single MASTER record. When a master record has not been adjusted to contain official data, the notification bar will indicate this.&#x20;

The **Advanced** view of the **Entity Relationship** panel shows the local records which have been used to represent the master record. For example, Gustavo Osorio's relationship with a mother record (Guerra) is inferred (indicated by the dotted line) via the local from a source system (indicated by a solid line). However, this relationship exists on one local, the other local does not have any information about Gustavo's mother.

![](<../.gitbook/assets/image (447) (1) (1).png>)

{% hint style="info" %}
Master records don't contain data beyond identifiers. They are abstract Entity objects which act as a linker between different sources of information.
{% endhint %}

#### Master with Record Of Truth

When a data administrator uses the administrative panel to edit a patient record, the administrative panel (granted with **Establish MDM Record of Truth**) will construct a new SOURCE/LOCAL record (which belongs to the administrative panel) which is promoted to **Record of Truth**. This will be indicated with a green bar and an option to view the ROT and/or EDIT the master.

![](<../.gitbook/assets/image (452) (1) (1).png>)

{% hint style="info" %}
All edits by the administrative panel to the MASTER record are redirected to the record of truth. It is recommended that administrators and data officers edit new official information on the ROT directly.
{% endhint %}

## Patient Details

The remainder of the patient detail screen is occupied by the patient demographics and information tabs. These tabs can be extended based on the plugins enabled on the SanteDB server.&#x20;

![](<../.gitbook/assets/image (451) (1) (1).png>)

By default the following tabs may appear based on your user access level:

* Demographics - Contains detailed information about the patient demographics contained in the current record.
* Master Data Management - (User requires MDM permissions) - Contains detailed information and controls related to the management of the MDM metadata attached to the record (if any)
* Data Quality - Contains information about issues related to the record. The data which appears in this tab will depend on the configuration of the data quality rules for the implementation (see: [data-quality-services.md](../operations/server-administration/host-configuration-file/data-quality-services.md "mention"))

## Related Topics

{% content-ref url="correcting-data/" %}
[correcting-data](correcting-data/)
{% endcontent-ref %}

{% content-ref url="../user-guides/santempi/the-patient-dashboard/master-data-management-tab.md" %}
[master-data-management-tab.md](../user-guides/santempi/the-patient-dashboard/master-data-management-tab.md)
{% endcontent-ref %}

{% content-ref url="../user-guides/santempi/the-patient-dashboard/data-quality-tab.md" %}
[data-quality-tab.md](../user-guides/santempi/the-patient-dashboard/data-quality-tab.md)
{% endcontent-ref %}
